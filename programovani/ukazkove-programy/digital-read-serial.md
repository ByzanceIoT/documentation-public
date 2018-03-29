# Digital Read Serial

Tento příklad ukazuje, jak monitorovat stav na tlačítku přes sériovou komunikaci mezi IODA a PC.

## Hardware
* IODA 
* tlačítko
* kabely
* 10kΩ rezistor
* nepájivé kontaktní pole

## Obvod
Do desky jsou zapojené tři kabely. První dva - černý a červený jsou zapojeny do GND a 3V3 pinu na desce. Třetí jde z pinu X01 na kontakt tlačítka, na protější kontakt připojíme  10kΩ rezistor na zem (GND). 3.3 voltu (3V3) připojíme na poslední kontakt vedle země (GND).

### Tlačítko

Stisknutím tlačítka, nebo přepínače se propojí dva body v obvodu. Když je tlačítko otevřeno (není stisknuto), nedojde k žádnému spojení mezi oběma kontakty tlačítka, takže kontakt je připojen k uzemnění (pomocí pull-down) a čte jako LOW nebo 0. Když je tlačítko zavřené (stisknuto), vytváří spojení mezi oběma kontakty, připojuje pin na 3.3 voltů tak, aby kontakt četl jako HIGH, nebo 1.

![](/assets/DigitalReadSerial.png)

## Schéma

![](/assets/DigitalReadSerial_schematic.png)

## Code
### init()
V první části programu se musí nastavit knihovny, seriová komunikace a vstup pinu X01. Ve funkci ```init()``` se nastaví modulační rychlost.
Zbytek programu už probíhá ve funkci ```loop()```.
### loop()
První věc, kterou je potřeba provést v hlavní smyčce programu, je načíst hodnotu na pinu X01, přicházející z vašeho přepínače. Vzhledem k tomu, že informace přicházející z přepínače budou buď "1", nebo "0", není potřeba používat jiný datový typ než int.

``` cpp
pc.printf("\n button value is : %d",button.read()); 
```
Tento příkaz načítá hodnotu tlačítka a nasledně ji vypíše na seriový monitor.

``` cpp
  /**DigitalReadSerial
    * This example shows you how to monitor the state of a switch
    * by establishing serial communication between
    * IODA and your computer over USB.
    */

#include "byzance.h"   // include libraries for IODA
Serial pc(SERIAL_TX, SERIAL_RX);
DigitalIn button(X01);   // Set the analog pin.
void init(){   // The init routine runs only once when you press reset.
  pc.baud(115200);   // Set baud rate.
}
void loop(){   // the loop routine runs over and over agin forever:
  pc.printf("\n button value is : %d",button.read());   // Read button value and print it.
  Thread::wait(100);   // Wait for 1000ms.
}


```