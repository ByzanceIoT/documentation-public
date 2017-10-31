## Struktura programu

Zařízení Byznce se programují v jazyce **C++** a využívají knihoven **MBED API** a **Byzance API**. Pro správnou funkčnost programu v Byzance zařízení je nutné importovat knihovnu Byzance API příkazem 

```cpp
#include "byzance.h"
```

Tato knihovna má za úkol automaticky inicializovat periferie, připojit zařízení k internetu a inicializovat vlákna, která se starají o update zdrojového kódu a připojení k serverům. Importem knihovny se také zpřístupní [funkce](/programovani/byzance-api/funkce.md) a [uživatelská makra](/programovani/byzance-api/uzivateska-makra) Byzance API.

### Definice fyzických vstupů a výstupů

Následně po importu všech potřebných knihoven, je v případě jejich použití nutné definovat fyzické vstupy a výstupy, které se budou v programu používat. Zařízení Byzance na své GPIO sběrnici disponují Analogovými i digitálními vstupy a výstupy.

```cpp
// Definice fyzických vstupů a výstupů
DigitalOut DI1(X02);
DigitalIn DO1(X05);
AnalogOut AO1(Y23);
AnalogIn AI1(Y22)
```

Bližší informace o fyzických vstupech a výstupech lze získat v [MBED API - Vstupy a výstupy](/programovani/mbed-api/vstupy-a-vystupy.md).

### Virtuální vstupy a výstupy 

Při programování funkčního bloku v pro tool [BLOCKO](odkaz na blocko)  

Po importu knihovny Byzance by měla následovat definice vstupů a výstupů pro , ale Code server si s tím poradí v celém main souboru.


Více viz [Byzance IO](/byzance_documentation/hardware_intro/API/byzance-io.md).

```cpp
//definice virtuálních vstupů a výstupů
```

V další části kódu se poté definují fyzické vstupy a výstupy desky viz [MBED vstupy a výstupy](/byzance_documentation/hardware_intro/API/mbed-api/vstupy-a-vystupy.md)


```cpp
// Definice fyzických vstupů a výstupů
DigitalOut D1(X02);
DigitalIn D2(X05);
AnalogOut A1(Y23);

```

Poté je vhodné inicializovat globální proměnné a objekty jako například sériová komunikace atd.

```cpp
Serial pc(SERIAL_TX_pin, SERIAL_RX_pin); // tx, rx
```

**TO DO - přeformulovat následující odstavec**
Po inicializaci proměnných je možné implementovat funkci pre\_init\(\). Tato funkce je spuštěna předtím, než je inicializováno vlákno Byzance a předtím než se zažízení připojí k serverům. Tuto funcki není nutné implementovat, nicméně je vhodná v případě debugu.

```cpp
void pre_init(){
   
}
```

Následuje inicializační část, která je automaticky zavolána právě jednou po startu zařízení.

```cpp
void init(){
    pc.printf("Hello world\n");
}
```
Poslední je část kódu, který se bude vykonávat ve smyčce. Slouží jako náhrada while\(true\) cyklu v klasické main funkci. Jediným rozdílem je to, že mezi každým loop\(\) se automaticky dává prostor i Byzance vláknu a [resetuje se watchdog](/byzance_documentation/hardware_intro/features/watchdog.md). 

```cpp
void loop(){
    pc.printf("Test\n");
    Thread::wait(500);
}
```

# Příklad

Jednoduchý kód pro výpis do sériové linky \(bez debugu\) může tedy vypadat například takto.

```cpp
#include "byzance.h"

// Definice fyzických vstupů a výstupů
DigitalOut D1(X02);
DigitalIn D2(X05);
AnalogOut A1(Y23);

Serial pc(SERIAL_TX, SERIAL_RX); // tx, rx

void init(){
    // Hello world se vypise jednou pri startu
    pc.printf("Hello world\n");
}

void loop(){
    // Test se bude vypisovat stale dokola kazdych 500 ms
    pc.printf("Test\n");
    Thread::wait(500);
}
```


