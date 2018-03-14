# Analog Read Serial

Tento příklad ukazuje, jak číst z analogického vstupu pomocí potenciometru. **Potenciometr** je jednoduché mechanické zařízení, které mění odpor v závislosti na změně hřídele vůči odporové dráze.
Průchodem napětí potenciometrem do analogového vstupu na desce lze měnit množství odporu, které se převede na analogovou hodnotu. V tomto příkladu monitoruje stav potenciometru po zavedení seriové komunikace mezi IODA a počítačem.



## Hardware

- 10kΩ potenciometr
- IODA
- LED
- 100Ω rezistor

## Obvod 

Pro přípojení potenciometru se použijí 3 vodiče. První vychází z vnějšího pinu potenciometru na zem. Druhá část vychází z druhého vnějšího pinu na 3.3 voltu. Třetí vychází ze středního pinu potenciometru na analogový pin Y25.
Pro zapojení LED se použijí 2 vodiče a jeden 100Ω rezistor.

![](/assets/upraveny_AnalogReadSerial1.PNG)
## Schéma
![](/assets/schema_AnalogReadSerial1.PNG)

## Code
### Komunikační rozhraní
 ```cpp
 Serial pc(SERIAL_TX, SERIAL_RX);  
 ```
Tato funkce slouží k definici sériového rozhraní a komunikaci po sériové lince. Ke komunikaci jsou zapotřebí dva piny - RX(recieve data) a TX(transfer data).

### Knihovny
 Na začátku každého programu se musí načíst potřebné knihovny. Jako základní knihovnu požíváme byzance.h.
 ```cpp
 #include "byzance.h"
 ```
 ### Analogový vstup (AnalogIn)
 Převede napětí na pinu analogového vstupu v rozmezí 0 - 3.3V do digitální podoby a interpretuje ho číslem na škále 0-4095. Rozlišení převodníku je 2.44 mV.
  ```cpp
 AnalogIn ain(pin_name);
printf(”ain value = %3.3f%%\n”, ain.read());
  ```

 ### Analogový výstup (AnalogOut)
 Funkce AnalogOut umožňuje definovat analogový výstup, který pomocí digitáně analogového převodníku dokáže na základě vstupní hodnoty této funkce měnit hodnotu napětí na výstupním pinu v rozsahu 0 - 3.3V . Procesor umožňuje definovat dva analogové výstupy, a to na pinech Y23 a Y25. Velikost napětí na výstupu je škálováno zápisem v rozsahu 0 - 1, kdy 1 je maximální napětí 3.3V.
  ```cpp
 //Definice analogového výstupu na pinu Y25
AnalogOut aout(Y25);

// Nastavení maximálního napětí
aout = 1.0f;

// Nastavení poloviny VCC
aout = 0.5f; 

// Čtení aktuální hodnoty napětí na 
aout.read();
  ```

 ### Funkce
 Funkce ``` init()``` se vyvolá při spuštění.Používa se pro inicializaci proměnných, pinových režimů apod. Funkce se spustí pouze jednou při spuštění nebo resetování desky.

 Funkce ```loop()``` se spustí až po funkci ```init()``` a opakuje se neustále dokola, což dovolí program měnit a kontrolovat za běhu. Používá se pro akční kontrolu desky.

 Jakýkoliv řádek, který začíná dvěma lomítky(//), kompilátor nečte, tudíž slouží k okomentování části programu, nebo-li pro vysvětlení co danná část kodu dělá.


 ```cpp
 void init{
    // nastavení programu, spustí se pouze jednou
 } 
 
 
 void loop{
    // hlavní program, opakuje se neustále dokola
 }
 ```
### Nastavení modulační rychlosti
 V programu (viz.níže) se provádí jedínný příkaz v init() funkci, jednotka modulační rychlosti 115200 bitů za sekundu.
```cpp
pc.baud(115200);
```

### Výpis hodnot

 ```cpp 
 pc.printf("ain value =%3.3f%%\n",ain.read());
 ```
Slouží k vzpání vypsání hodnot z potenciometru na seriový monitor.



### Pozastavení programu 
 ```cpp
 Thread::wait(100);
 ``` 
Slouží k pozastavení programu na 100ms.

```cpp

  /**AnalogOutInSerial
    * Reads an analog input pin, maps the result to a range from 0 to 1 and uses
    * the result to set the pulse width modulation (PWM) of an output pin.
    * Also prints the results to the Serial Monitor.
    */
    
#include "byzance.h"   // Include libraries for IODA.

Serial pc(SERIAL_TX, SERIAL_RX);   // Defines the comunication interface if the serial line , SPI, CAN is needen in the program.

AnalogOut aout(Y25);   

AnalogIn ain(Y23);

// the init routine runs only once when you press reset:
void init(){

  
  pc.baud(115200);   // set baud rate.
}
// the loop routine runs over and over agin forever:
void loop(){ 

  pc.printf("ain value =%3.3f%%\n",ain.read());
  
  aout=ain; 
  
  Thread::wait(100);   // Wait for 100ms.
  
}


```