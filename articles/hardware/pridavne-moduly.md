# Serial shield \(B1\)

Shield slouží jako převodník mezi sběrnicemi UART - RS-232 \(plně duplexní\) nebo UART - RS-485 \(poloduplexní\).

![](/assets/serial_b1_b.png)

## Hardware

### Zapojení X konektoru

| **X01** | **X03** | **X05** | **X07** | **X09** | **X11** | **X13** | **X15** | **USR** | **VBUS** |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :--- |
|  |  |  |  | TTL\_RX | TTL\_TX |  |  |  |  |
| **X00** | **X02** | **X04** | **X06** | **X08** | **X10** | **X12** | **X14** | **3V3** | **GND** |
|  |  |  |  |  |  | DIR |  |  |  |

* _TTL\_RX_ - slouží pro příjem na sběrnici RS-232 i RS-485
* _TTL\_RX_ - slouží pro vysílání na sběrnici RS-232 i RS-485
* _DIR_ - volba směru na sběrnici RS-485

### Konfigurace a zapojení

Jsou k dispozici dvě jumperové propojky:

* _J1_ - volba RX pinu \(vlevo RS-485, vpravo RS-232\)
* _J2_ - volba TX pinu \(vlevo RS-485, vpravo RS-232\)
* _X2_ - konektor pro připojení na sběrnici RS-485
* \_X3 - \_konektor pro připojení na sběrnici RS-232

## Software

### Příklad prgramu pro RS-485

```cpp
#include "byzance.h"

Serial    pc(X11, X09); // tx, rx
DigitalOut dir(X12);
DigitalOut ledRed(LED_RED);

int i = 0;

void init(){
    pc.baud(115200);
    pc.printf("Hello world from serial test\n");

}

void loop(){
    ledRed = !ledRed;
    dir=1;
    pc.printf("serial test = %d\n", i);
    dir=0;
    i++;
    Thread::wait(500);
}
```

# LED shield \(B1\)

Shield slouží k zobrazení dat pomocí trojmístného sedmisegmentového displeje, LED diod či bargrafu, RGB diod nebo pomocí LED pásku.

![](/assets/shield_led_b1.png)

## Hardware

### Zapojení X konektoru

| **X01** | **X03** | **X05** | **X07** | **X09** | **X11** | **X13** | **X15** | **USR** | **VBUS** |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :--- |
|  |  |  | SDA |  |  |  |  |  | &gt; 6V |
| **X00** | **X02** | **X04** | **X06** | **X08** | **X10** | **X12** | **X14** | **3V3** | **GND** |
| BTN |  |  | SCL |  |  |  | DAT | 3.3 V | GND |

* _SCL_ a _SDA_ - komunikace po I2C sběrnici s expandery pro řízení LED diod, displeje a RGB displeje
* _DAT_ - datový vodič pro LED pásky
* _BTN_ - tlačítko

### Konfigurace a zapojení

* _X3_ - svorkovnice pro připojení LED pásku \(5 V, GND a datový vodič\) s ředičem WS2812\); datový vodič chráněn rezistorem, proudová pojistka pro 5 V \(1 A\)
* _LED2 - LED11_ - LED diody pro zobrazení bargrafu 
* _LED1 _- trojmístný sedmisegmentový displej
* _D1, D2_ - RGB LED diody
* _3 V_ - detekce napětí 3,3 V
* _5 V_ - detekce 5 V napájení
* SJ1, SJ2 - volba napájení pro LED pásek

## Software

```cpp
#include "byzance.h"
#include "TripleSevenSeg.h"
#include "TLC59116.h"

#define BYZANCE_OVER_USB 0

#if BYZANCE_OVER_USB
    USBSerial    usb(0x1f00, 0x2012, 0x0001, false);
#else
    Serial        pc(SERIAL_TX, SERIAL_RX); // tx, rx
#endif

// Common variables
uint32_t tmp32 = 0;
InterruptIn btnUsr(USER_BUTTON);
volatile bool button_usr_clicked= 0;
uint32_t i = 0;

// Object for LED segment display and LED bargraph
TripleSevenSeg * seven_segment;
TLC59116 * pwm_driver;


/*
 * Prototyp, který bude vybírat, kam se konzole vypisuje
 */
void to_computer(const char* format, ...);

void button_usr_fall_callback(){
    button_usr_clicked = 1;
}

void init(){

#if BYZANCE_OVER_USB
    ByzanceLogger::init(&usb);
#else
    ByzanceLogger::init(&pc);
    pc.baud(115200);
#endif

    // Attach callback for user button
    btnUsr.fall(&button_usr_fall_callback);

    // sSven_segment
    seven_segment = new TripleSevenSeg();
    seven_segment->is_initialized();
    Thread::wait(100);

    // PWM driver init
    pwm_driver = new TLC59116();
    pwm_driver->initialize(X07, X06);     // I2C SDA, I2C SCL
}

void loop(){

    // Change global PWM dimming
    if(button_usr_clicked){
        button_usr_clicked=0;
        to_computer("Button pressed.\n");
        pwm_driver->set_global_pwm(((i % 2) == 0) ? 2 : 0xFF);    // Choose 2 or 255 global PWM value.

    }

    // Display generated numbers from negativ to positive values with maximally two decimal digits.
    seven_segment->display_number(-120 + ((float)i++)/1 + 0.12, 2);

    // PWM dimming of the LED bargraph
    uint8_t pole[16];
    for (uint8_t j = 0; j < 16; j++) {
        pole[j] = i*5;
    }
    pwm_driver->set_all_channels(pole);

    // Wait some time
    Thread::wait(50);
}


void to_computer(const char* format, ...){
    char buffer[256];

    va_list arg;
    va_start (arg, format);
    vsnprintf(buffer, 256, format, arg);
    va_end (arg);

    #if BYZANCE_OVER_USB
        usb.printf(buffer);
    #else
        pc.printf(buffer);
    #endif
}
```

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
 * @param	none
 * @return	prepocitana vzdalenost v cm
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

    return timer.read_us()/58;  			// prepocet na vzdalenost v cm
}
```



