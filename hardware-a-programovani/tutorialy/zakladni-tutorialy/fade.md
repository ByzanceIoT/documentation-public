# Fade

Tento příklad demonstruje použití funkce PwmOut ke stmívání LED diody. PwmOut využívá pulzně šířkovou modulaci \(PWM\), pomocí, které lze modulovat analogovou hodnotu napětí na digitálním výstupu. 

## Použitý hardware

* IODA
* 220Ω rezistor
* LED
* kabely
* nepájivé kontaktní pole

## Schéma zapojení

[Anoda](https://cs.wikipedia.org/wiki/LED#/media/File:%2B-_of_LED_2.svg) LED je zapojena na pin Y25 přes 220Ω resistor. [Katoda](https://cs.wikipedia.org/wiki/LED#/media/File:%2B-_of_LED_2.svg) je připojena k zemi \(pinu GND\). 

![](../../../.gitbook/assets/untitled-page-001-2%20%281%29.jpg)

![](../../../.gitbook/assets/fade-fritzing%20%281%29.PNG)

## Funkce 

LED se stmívá a rozsvicí díky změně nastavení **PWM** která se mění v cyklu **for.**   
Aby LED zhasla a rozsvítila postupně se zvětšuje PWM z 0 \(úplně vypnuto\) na 1 \(zapnuto\) a pak  
 znovu na 0. Pokaždé se přes smyčku zvyšuje o hodnotu proměnné offset.

## Code

je-li proměnná brightness na jedné z koncových hodnot \(buď 0 nebo 1\), změní se fadeAmount na negativní. Jinými slovy, pokud je`offset=0,01;` pak je nastavena na -0,01. Pokud je hodnota `offset=-0,01;`, pak je nastavena na hodnotu 0,01.

```cpp
/**Fade
  *This example shows how to fade an LED on pin Y25 using the
  *PWM function.
  */
#include "byzance.h"   // Include libraries for IODA
Serial pc(SERIAL_TX, SERIAL_RX);   // Defines the comunication interface if the serial line , SPI, CAN is needen in the program.
PwmOut aout(Y25);   // Set pin Y25 for led.
void init(){   // The init routine runs only once when you press reset.
    pc.baud(115200);   // Set baud rate.
}
void loop(){   // The loop routine runs over and over agin forever

     for(float offset=0.0; offset<=1; offset+=0.01) {
        aout.write(0.005 + offset);
        Thread::wait(25);
     }

     for (float offset = 1.0 ; offset >= 0 ; offset -= 0.01) {
        aout.write ( 0.005 + offset );
        Thread::wait(10);
     }

}
```



 V hlavičce programu je nutné importovat knihovny [Byzance Hardware API](https://docu.byzance.cz/hardware-a-programovani/programovani-hw/byzance-api) a [Mbed API](https://docu.byzance.cz/hardware-a-programovani/programovani-hw/mbed-api). pomocí

```cpp
 #include "byzance.h"
```

 Poté nasleduje konstruktor definující objekt [sériové linky](https://docu.byzance.cz/hardware-a-programovani/tutorialy/komunikace-po-seriove-lince-uart-s-pc).

```cpp
 Serial pc(SERIAL_TX, SERIAL_RX);
```

Nastavení PWM výstupu na pinu Y25 .

```cpp
PwmOut aout(Y25);   // Set pin Y25 for led.
```

  
Při každém spuštění programu se nejprve provede funkce _**init\(\)**,_ která primárně slouží k inicializaci všech objektů a proměnných.V tomto programu pouze inicializujeme rychlost sériové linky.

```cpp
void init(){   // The init routine runs only once on the begin of the program
  pc.baud(115200);   // Set baud rate.
}
```

Cyklus **for** je řídicí struktura počítačového programu a je svou činností podobný cyklu while-do s testováním podmínky na začátku cyklu.

```cpp
     for(float offset=0.0; offset<=1; offset+=0.01) {
        aout.write(0.005 + offset);
        Thread::wait(25);
     }
```

 Uvnitř samotného cyklu se do proměnné **aout** přidává analogová hodnota 0.005  + **offset** která je zvětšována o 0.01 každých 25ms. 

```cpp
aout.write(0.005 + offset);
```

