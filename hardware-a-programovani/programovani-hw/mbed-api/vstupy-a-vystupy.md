# Vstupy a výstupy

## Vstupy a výstupy

V této sekci jsou zdokumentovány funkce z knihovny MBED API, sloužící k ovládání fyzických vstupů a výstupů GPIO sběrnice zařízení Byzance.

## AnalogIn

Převede napětí na pinu analogového vstupu v rozmezí 0 - 3.3V do digitální podoby a interpretujep ho číslem na škále 0-4095. Rozlišení převodníku je 2.44 mV.

```cpp
#include "byzance.h"

#define SUPPLY_VOLTAGE 3.3

AnalogIn ain(X00);

void loop(){
	printf("voltage on pin X00 is %d V\n",ain.read()*SUPPLY_VOLTAGE);
	Thread::wait(1000);
}
```

## AnalogOut

Funkce **AnalogOut** umožňuje definovat analogový výstup, který pomocí digitáně analogového převodníku dokáže na základě vstupní hodnoty této funkce měnit hodnotu napětí na výstupním pinu v rozsahu **0 - 3.3V** . Velikost napětí na výstupu je škálováno zápisem v rozsahu **0 - 1**, kdy 1 je maximální napětí 3.3V.

```cpp
#include "byzance.h"

AnalogOut aout(Y23);

void loop(){
	aout = 1.0;		//setting supply voltage on pin Y23
	Thread::wait(200);
	aout = 0.5;		//setting half of supply voltage on pin Y23
	Thread::wait(1000);
}
```

## DigitalIn

Přečte hodnotu digitálního vstupu

```cpp
#include "byzance.h"

DigitalIn din(USR);

void loop(){
	if(din.read() == 1){
		printf("button is pressed\n");
	else{
		printf("button is not pressed\n");
	Thread::wait(1000);
}
```

## DigitalOut

Nastaví na digitálním vástupu logickou úroveň.

```cpp
#include "byzance.h"

DigitalOut dout(LED_BLUE);

void init(){
    Byzance::led_module(false);  	//disable LED module for Byzance
}

void loop(){
	dout = !dout;				//read the value, invert it and store again
	Thread::wait(1000);
}
```

## DigitalInOut

Obousměrný digitální pin, kombinace digitálního vstupu a digitálního výstupu.

```cpp
DigitalInOut diout(pin_name);

// configure as output
diout.output();

// set HIGH
diout = 1;

// configure as input
diout.input();

// read value of pin
pc.printf("diout value = %d \n", diout.read());
```

## BusIn

Funkcí BusIn lze vést libovolný počet digitálních vstupů jako bus, což umožňuje přečíst digitální hodnotu těchto vstupů jako jedno číslo.

```cpp
#include "byzance.h"

BusIn switches(X01,X02,USR);	//bus is defined X01, X02 and USR button

void init(){
	switches.mode(PullDown);	//set all pins as pull-down
}

void loop(){
	switch(switches.read()){	//switch according to bus state	
		case 0x0: printf("X01-DOWN X02-DOWNW USR-not-pressed\n"); break;
		case 0x1: printf("X01-UP X02-DOWN USR-not-pressed\n"); break;
		case 0x2: printf("X01-DOWN X02-UP USR-not-pressed\n"); break;
		case 0x3: printf("X01-UP X02-UP USR-not-pressed\n"); break;
		case 0x4: printf("X01-DOWN X02-DOWN USR-pressed\n"); break;
		case 0x5: printf("X01-UP X02-DOWN USR-pressed\n"); break;
		case 0x6: printf("X01-DOWN X02-UP USR-pressed\n"); break;
		case 0x7: printf("X01-UP X02-UP USR-pressed\n"); break;
	}
	Thread::wait(500);
}
```

## BusOut

Třída BusOut definuje z libovolného počtu digitálních výstupů výstupní sběrnici.  Na sběrnici je pak možné jednoduše zapisovat. 

```cpp
#include "byzance.h"

BusOut leds(LED_BLUE,LED_RED,LED_GREEN);	//bus is defined by all RGB LED

void init(){
    Byzance::led_module(false);  		//disable LED module for Byzance
}

void loop(){
	for(uint8_t i = 0; i < 8; i++){		//for each combination on bus
		leds = i;						//write color on bus
		Thread::wait(1000);
	}
}
```

## BusInOut

Definuje bus, ze kterého je možné jak číst, tak do něj i zapisovat.

```cpp
BusInOut io_bus(X01, X02, X03);

void loop(){

  io_bus.output(); // Nastaví bus na BusOut
  io_bus = 5;
  wait(5);
  io_bus.input();  // Nastaví bus na BusIn
  wait(5);
  if(io_bus == 0x6){
    printf("NUMBER 6!\n");
  }
}
```

## PortIn

PortIn má stejnou funkci jako BusIn, je o dost rychlejší ale méně flexibilnější

```cpp
// Argumentem konstruktoru je číslo portu a číslem určené piny tohoto portu
PortIn p2(port2, 0x0000003F); // pin 21 - 26  

void init(){
  //Nastavení módu portu
  p2.mode(PullNone); 
}
void loop(){
  int pins = p.read();
  if(pins){ //alespoň jeden vstup z portu má hodnotu jedna
    printf("At least one switch is turned on");
  }
}
```

## PortOut

Port Out nahrazuje BusOut, stejně jako PortIn je rychlejší ale méně flexibilnější

```cpp
#define LED_SHIELD 0x00B40000

PortOut port(Port2, LED_SHIELD);

void loop(){
  port=LED_MASK;
  wait(1);
  port=0;
  wait(1);

}
```

## PortInOut

Třída PortInOut kombinuje funkce PortIn a PortOut a mód této funkce lze nastavovat za běhu programu.

```cpp
#define LED_SHIELD 0x00B40000
PortOut port(Port2, LED_SHIELD);

void loop(){
  port.input();
  int port_value = port;
  port.output();
  port=LED_MASK;
  wait(1);
  port=0;
  wait(1);

}
```

## PwmOut

Funkce PwmOut umožňuje na pinu vytvářet pulzně šířkovou modulaci, regulovat její periodu a šířku jejich pulsů.

```cpp
PwmOut pwm(X04);

void loop(){

  pwm.period(4.0f);  //Natavení periody 4s 
  pwm.write(0.50f);  //50% duty cycle, vzhledem k periodě

  wait(10);

  pwm.period(4.0f);   //nastavení periody 4s
  pwm.pulsewidth(2);  //dvouvteřinový puls -> stejné jako 50% duty cycle


}
```

## InterruptIn

Funkce InterruptIn umožňuje uživateli okamžitě reagovat na změnu logické úrovně libovolného pinu \(na náběžnou i sestupnou hranu\) a na základě této změny zavolat libovolnou funkci.

```cpp
#include "byzance.h"

InterruptIn button(USR); //InterruptIn on USR button
DigitalOut led(LED_BLUE);

void pushed_button(){
    led = 1;		//on pushed button, turn on blue LED
}

void released_button(){
    led = 0;		//on released button, turn off blue LED
}

void init(){
    Byzance::led_module(false);  	//disable LED module for Byzance
    button.fall(&pushed_button);	//attach pusehed_button function on rising edge
    button.rise(&released_button);	//attach released_button function on falling edge
}

void loop(){
	printf("im running!\n");
	Thread::wait(1000);
}
```

