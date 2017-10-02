# Struktura programu

Základem při psaní zdrojového kódu je využití open-source operačního systému [MBED-OS](/byzance_documentation/hardware_intro/API/mbed-api.md). Kód se píše především v online rozhraní Becki Byzance.

V první části programu, nejlépe již na prvním řádku, je nutné importovat knihovnu Byzance pomocí pžíkazu:

```cpp
#include "byzance.h"
```
Tato knihovna má za úkol automaticky inicializovat periferie, připojit desku k internetu a inicializovat vlákna, která se starají o update zdrojového kódu a připojení k serverům. Includem knihovny se zpřístupní [Byzance API](/byzance_documentation/hardware_intro/API/byzance-api.md) a [uživatelská makra](/byzance_documentation/hardware_intro/API/makra.md).

Následovat by měla definice vstupů a výstupů pro blocko, ale Code server si s tím poradí v celém main souboru.

Více viz [Byzance IO](/byzance_documentation/hardware_intro/API/byzance-io.md).

```cpp
//definice virtuálních vstupů a výstupů
```

v další části kódu se poté definují fyzické výstupy a vstupy desky viz [MBED vstupy a výstupy](/byzance_documentation/hardware_intro/MBED API/vstupy-a-vystupy.md)


```cpp
//definice vstupů a výstupů
DigitalOut D1(X02);
DigitalIn D2(X05);
AnalogOut A1(Y23);

```

Inicializace globálních proměnných a objektů, například sériová linka atd.

```cpp
Serial pc(SERIAL_TX_pin, SERIAL_RX_pin); // tx, rx
```



Věci ve funkci pre\_init\(\) se pustí dříve, než Byzance vlákno a připojení k serverům. Nepovinná část spíše nutná pro debug.

```cpp
void pre_init(){
   
}
```

Inicializační část, která je automaticky zavolána právě jednou po startu zařízení.

```cpp
void init(){
    pc.printf("Hello world\n");
}
```

Poslední je část kódu, který se bude vykonávat stále dokola, slouží jako náhrada while\(true\) cyklu v klasické main funkci. Jediným rozdílem je to, že mezi každým loop\(\) se automaticky dává prostor i Byzance vláknu a [resetuje se watchdog](/byzance_documentation/hardware_intro/features/watchdog.md).

```cpp
void loop(){
    pc.printf("Test\n");
    Thread::wait(500);
}
```

# Příklad

Jednoduchý kód pro výpis do sériovky \(bez debugu\) může tedy vypadat takto

```cpp
#include "byzance.h"

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



