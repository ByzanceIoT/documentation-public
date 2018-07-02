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

U **PWM** lze nastavit dva parametry - **frekvenci a střídu**. **Frekvence** nastavuje periodu pulzů a v tomto příkladě jí nastavíme dostatečně vysokou, aby lidské oko nebylo schopné zaznamenat rychlé blikání s LED diodou. **Střída** nastavuje poměr mezi zapnutím a vypnutím, tedy dobou, kdy je během jedné periody digitální výstup nastaven na logickou úroveň 1 a logickou 0. Tato hodnota určuje stmívání LED. V následujícím programu je nastavena fixní perioda na 0,01s \(100Hz\) a postupnou změnou střídy se LED dioda nejprve rozsvěcí a poté stmívá. 

## Code

```cpp
/**Fade
  *This example shows how to fade an LED on pin Y25 using the
  *PWM function.
  */
#include "byzance.h"   // Include libraries for IODA
Serial pc(SERIAL_TX, SERIAL_RX);   // Defines the comunication interface if the serial line , SPI, CAN is needen in the program.
PwmOut aout(Y25);   // Set pin Y25 for led.
void init(){   // The init routine runs only once when you press reset.
    pc.baud(115200);     // Set baud rate.
    aout.period(0.01f);  // Set the period(frequency) of PWM output to 0,01s (100Hz)
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

  
Při každém spuštění programu se nejprve provede funkce _**init\(\)**,_ která primárně slouží k inicializaci všech objektů a proměnných.V tomto programu inicializujeme rychlost komunikace sériové linky a nastavujeme frekvenci PWM na 100Hz.

```cpp
void init(){   // The init routine runs only once on the begin of the program
  pc.baud(115200);     // Set baud rate.
  aout.period(0.01f);  // Set the period(frequency) of PWM output to 0,01s (100Hz)
}
```

v hlavní smyčce `loop()` poté definujeme cyklus **for**, ve kterém postupně zvyšujeme střídu PWM na výstupu **aout**, čímž rozsvěcíme LED diodu. Obdobný cyklus později využíváme i ke zmenšování střídy \(stmívání LED\).

```cpp
     for(float offset=0.0; offset<=1; offset+=0.01) {
        aout.write(0.005 + offset);
        Thread::wait(25);
     }
```

 Změnu hodnoty střídy PWM aout provádíme pomocí příkazu 

```cpp
aout.write(0.005 + offset);
```

