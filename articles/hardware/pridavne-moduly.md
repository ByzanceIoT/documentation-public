
# Ultrasonic shield \(B1\)

Shield slouží k měření vzdálenosti pomocí odrazu akustického signálu od měřeného objektu.

![](/assets/shield_ultrasonic_b1.png)

## Hardware

### Zapojení X konektoru

| **X01** | **X03** | **X05** | **X07** | **X09** | **X11** | **X13** | **X15** | **USR** | **VBUS** |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :--- |
|  | ECHO |  |  |  |  |  |  |  |  |
| **X00** | **X02** | **X04** | **X06** | **X08** | **X10** | **X12** | **X14** | **3V3** | **GND** |
|  | TRIG |  |  |  |  |  |  | 3.3 V | GND |

* _ECHO_ - pin pro potvrzení spuštění měření a detekci jejího dokončení
* _TRIG_ - pin pro spuštění měření
* _5V_ - detekce 5 V napájení ze step-up regulátoru
* 3_V_ - detekce 3.3 V napájení pro step-up regulátor

### Konfigurace a zapojení

## Software

```cpp
#include "byzance.h"

/*
 * Test_ultrazvuk
 * napajeni MUSI byt +5V0, na +3V3 to nefunguje
 */

// seriovka
Serial pc(SERIAL_TX, SERIAL_RX);

// ultrazvuk TRIG na X06
DigitalOut trig(X02);

// ultrazvuk ECHO na X04 (jsou tam pripadne i timery T3CH3, T1CH2N)
DigitalIn echo(X03);

// timer
Timer timer;

DigitalOut ledRed(X00);
DigitalOut ledGrn(X01);

// vzdalenost v cm
int distance_cm;

bool measuring = 0;

int getDistance(void);


void loop() {

    distance_cm = getDistance();

    if(distance_cm > 400 || distance_cm < 1){
        pc.printf("Out of range\n");
    } else {
        pc.printf("Distance = %d cm\n", distance_cm);
    }

    Thread::wait(1000);
}


/**
 * Vysle 10us pulz na TRIG a meri sirku pulzu vracenou na ECHO
 * @param    none
 * @return    prepocitana vzdalenost v cm
 *
 */
int getDistance(void){

    // 10 microsecond pulse
    trig = 1;
    wait_us(10);
    trig = 0;

    // reset timer
    timer.reset();

    while(!echo){
        // waiting too long for rising edge
        if(timer.read_ms()>100) return 0;
    }

    // reset timer
    timer.reset();

    while(echo){
        // waiting too long for falling edge
        if(timer.read_ms()>100) return 0;
    }
    //timer.stop();

    return timer.read_us()/58;              // prepocet na vzdalenost v cm
}
```

# Meteo shield \(B1\)

Shield slouží k měření různých \(meteorolických\) veličin: teplota \(až 3x\), vlhkost, atmosferický tlak a osvětlení.

![](/assets/shield_meteo_b1.png)

## Hardware

### Zapojení X konektoru

| **X01** | **X03** | **X05** | **X07** | **X09** | **X11** | **X13** | **X15** | **USR** | **VBUS** |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :--- |
|  |  | PT1000 | SDA |  |  |  |  |  |  |
| **X00** | **X02** | **X04** | **X06** | **X08** | **X10** | **X12** | **X14** | **3V3** | **GND** |
|  |  | LIGHT | SCL |  |  |  |  | 3.3 V | GND |

* PT1000 - analogový vstup pro detekci odporu senzoru Pt1000
* LIGHT -analogový vstup pro detekci intenzity okolního osvětlení
* SDA a SCL - komunikace po I2C sběrnici se senzory
* 3_V_ - detekce 3.3 V napájení pro step-up regulátor

### Konfigurace a zapojení

* _SJ1 - _spojením se připojí analogový výstup pro detekci osvětlení
* _SJ2 -_ spojením se připojí analogový výstup pro měření teploty pomocí senzoru Pt1000
* _JP1 -_ konektor pro připojení senzoru Pt1000
* _R1_ - nastavení citlivost senzoru osvětlení
* _D1_ - detekční fotodioda senzoru okolního osvětlení
* _IC1, IC2_ - integrované obvody pro měření tlaku, vlhkosti a tlaku

## Software

```cpp
#include "byzance.h"
#include "ms5637.h"
#include "SHT21_ncleee.h"
#include "DHT.h"

//initiate I2C for SHT21
I2C i2c(X07,X06);
SHT21 sht(&i2c);
AnalogIn   light(X05);
AnalogIn   pt1000(X04);
//initiate I2C for MS5637
ms5637 ms(X07,X06);

//initiate AM2302 sensor
//DHT sensor(X10, AM2302);
/*
 * konstanty pro vypocet odporu snimace Rt
 *
 * A - zesileni neinvertujiciho stupne
 * R - ve schematu R4
 * Rt = R*(1 - 4*(p - 0,5)/A)
 */
#define PT1000_A 3.2			//1+R6/R8
#define PT1000_R 1200			//R4


/*
 * konstanty prevod Rt -> t
 * linearizace prevodni tabulky pro Pt1000
 * t = K*Rt + q
 */
#define PT1000_K 0.2616828		//umera
#define PT1000_Q -261.12319		//posun po ose y

Serial		pc(SERIAL_TX, SERIAL_RX); // tx, rx

int rh, temp;
//int error;
float relHumidity, temperature;
int userRegister;

void init(){


	pc.baud(115200);

	ms.cmd_reset();	// reset MS5637
}

void loop(){


	/*
	 * reading data from  MS5637
	 * pressure and temperature
	 */
	float t = ms.calcTemp();
	float p = ms.calcPressure();
	float h=-1;
	pc.printf("ms5637: t = %2.2f\t p = %4.f\t h= %2.2f\n", t,p,h);

	/*
	 * reading data from  SHT21
	 * temperature and humidity
	 */
    t = sht.readTemp();
    h = sht.readHumidity();
    p=-1;
    pc.printf("sht21:  t = %2.2f\t p = %4.f\t h= %2.2f\n", t,p,h);
    pc.printf("light = %d\n",32768-light.read_u16());
    static float filtered=0;
    for(uint8_t i=0; i<16; i++){
		float pom = pt1000.read();
		float r = PT1000_R*(1-4*(pom-0.5)/PT1000_A);
		t=PT1000_K*r+PT1000_Q;
		filtered=t*0.2+filtered*0.8;
    }
    pc.printf("pt1000 tf = %f\n",filtered);



    Thread::wait(100);
}
```





