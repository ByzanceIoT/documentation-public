# Fade

Tento příklad demonstruje použití funkce PwmOut pro vypnutí a zapnutí LED. PwmOut využívá modulaci šířky impulzů \(PWM\), které velmi rychle zapíná a vypíná digitální pin s jiným poměrem mezi zapnutou a vypnutou částí, čímž se vytvoří efekt blednutí.Jelikož se v hlavím programu neuvádí frekvence PWM je nastavena na záklaní-50Hz.

## Použitý hardware

* IODA
* 220Ω rezistor
* LED
* kabely
* nepájivé kontaktní pole

## Schéma zapojení

Připojte anodu \(delší, pozitivní kontakt\) své LED na analogový výstupní pin Y25 na desce prostřednictvím 220 ohmového rezistoru. Připojte katodu \(kratší, záporný kontakt\) přímo k zemi.

![](../../../.gitbook/assets/aread-page-001.jpg)

![](../../../.gitbook/assets/fade-fritzing.PNG)

## Funkce 

LED bledne a rozsvicí se díky díky změně nastavení **PWM** která se mění v cyklu **for.**   
Aby LED zhasla a zapnula se, postupně zvětšete hodnotu PWM z 0 \(úplně vypnuto\) na 1 \(zapnuto\) a pak znovu na 0, abyste cyklus dokončili. V náčrtu níže je hodnota PWM nastavena pomocí proměnné nazvané brightness. Pokaždé se přes smyčku zvyšuje o hodnotu proměnné fadeAmount.

## Code

je-li proměnná brightness na jedné z koncových hodnot \(buď 0 nebo 1\), změní se fadeAmount na negativní. Jinými slovy, pokud je `fadeAmount=0,01;` pak je nastavena na -0,01. Pokud je hodnota `fadeAmount=-0,01;`, pak je nastavena na hodnotu 0,01.

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
        wait(0.25);
     }

     for (float offset = 1.0 ; offset >= 0 ; offset -= 0.01) {
        pwm.write ( 0.005 + offset );
        Thread::wait(10);
     }

}
```

Cyklus **for** je řídicí struktura počítačového programu a je svou činností podobný cyklu while-do s testováním podmínky na začátku cyklu.  
 Uvnitř samotného cyklu se do proměnné **aout** přidává analogová hodnota 0.005  + **offset** která je zvětšována o 0.01 každých 25ms. 

```cpp
     for(float offset=0.0; offset<=1; offset+=0.01) {
        aout.write(0.005 + offset);
        Thread::wait(25);
     }
```

