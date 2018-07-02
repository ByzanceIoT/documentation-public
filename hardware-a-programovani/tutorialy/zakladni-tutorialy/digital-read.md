# Digital Read

Tento příklad ukazuje, jak monitorovat stav stisknutí tlačítka přes sériovou linku mezi IODA a PC.

## Použitý hardware

* IODAG3E
* tlačítko
* kabely
* 10kΩ rezistor
* nepájivé kontaktní pole

## Schéma zapojení

Tlačítko SW1 připojíme mezi pin X01 a zem GND, dále připojíme pullup rezistor R1 o nominální hodnotě 1K mezi pin X01 a pin 3V3.

![](../../../.gitbook/assets/schema_pullup%20%282%29.png)

![](../../../.gitbook/assets/digittalreadserial-fritz%20%281%29.PNG)

## Funkce

Ve stavu, kdy je tlačítko rozepnuto, z pinu 3V3 do pinu X01 neprotéká teoreticky žádný proud \(prakticky velmi malý proud\). To z toho důvodu, že pin X01 je nastaven jako **Digital Input** a má velmi vysoký vstupní odpor. V takovém případě je na napětí na pinu X01 rovno napětí 3V3. V případě, že stiskneme tlačítko, začne protékat proud z pinu 3V3 přes rezistor R1 do země \(pinu GND\). V takovém případě je na X01 stejný potenciál jako na pinu GND, tedy napětí rovno 0V.

## Code

```cpp
#include "byzance.h"  // Include Byzance Hardware API and Mbed APU 

/**DigitalReadSerial
* This example shows you how to monitor the state of a switch
* by establishing serial communication between
* IODA and your computer over USB.
*/

Serial pc(SERIAL_TX, SERIAL_RX);
DigitalIn button(X01);   // Set the digital input pin.

void init(){   // The init routine runs only once on the begin of the program
  pc.baud(115200);   // Set baud rate.
}

void loop(){   // the loop routine runs forever :

  if(button.read() == 0){
    pc.printf("button is pushed \n"); 
  }else{
    pc.printf("button is not pushed \n");
  }

  Thread::wait(100);   // Wait for 100ms.
}
```

V hlavičce programu je nutné importovat knihovny [Byzance Hardware API](../../programovani-hw/byzance-api/) a [Mbed API](../../programovani-hw/mbed-api/). pomocí

```cpp
#include "byzance.h"
```

Poté nasledují dva konstruktory definující objekt [sériové linky](../komunikace-po-seriove-lince-uart-s-pc/) a objekt [digitálního vstupu](../../programovani-hw/mbed-api/).

```cpp
Serial pc(SERIAL_TX, SERIAL_RX); 
DigitalIn button(X01);   // Set the digital input pin.
```

Při každém spuštění programu se nejprve provede funkce _**init\(\)**,_ která primárně slouží k inicializaci všech objektů a proměnných.V tomto případě pouze inicializujeme rychlost komunikace sériové linky.

```cpp
void init(){   // The init routine runs only once on the begin of the program
  pc.baud(115200);   // Set baud rate.
}
```

V samotném programu, tedy v nekonečné smyčce _**loop\(\)**_, poté kontrolujeme stav stisknutí tlačítka pomocí funkce _**read\(\)**_ a na základě toho rozhodujeme, kterou zprávu vypsat do sériové linky.

```cpp
if(button.read() == 0){
    pc.printf("button is pushed \n"); 
  }else{
    pc.printf("button is not pushed \n");
  }
```

V poslední části kódu je vlákno programu uspáno na 100 milisekund.

```cpp
 Thread::wait(100);   // Wait for 100ms.
```

