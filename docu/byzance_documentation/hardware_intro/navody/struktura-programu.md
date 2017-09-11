# Struktura programu

Základem při psaní zdrojového kódu je využití open-source operačního systému \[\[tutorial:mbed\| MBED-OS\]\]. Kód se píše především v online rozhraní Byzance. 

Struktura je následovná. Na prvním řádku by měl být include byzance knihovny. Ta se postará o automatickou inicializaci periferií, připojení desky k internetu a zapnutí vláken, která se starají o update zdrojového kódu a připojení k serverům. Zároveň podporuje některá \[\[tutorial:macros\|uživatelská makra\]\] a \[\[tutorial:public\_functions\|rozhraní pro uživatele\]\].

```cpp
#include "byzance.h"
```

Následovat by měla definice vstupů a výstupů pro blocko, ale Code server si s tím poradí v celém main souboru.

Více viz \[\[tutorial:byzance\_io\| Byzance vstupy a výstupy viditelné z Blocka\]\]

```
Byzance vstupy a výstupy
```

Inicializace globálních proměnných a objektů

Například sériovka atd.

```
Serial pc(SERIAL_TX, SERIAL_RX); // tx, rx
```

Nepovinná část spíše nutná pro debug.

Věci ve funkci pre\_init\(\) se pustí dříve, než Byzance vlákno a připojení k serverům.

```cpp
void pre_init(){
    ByzanceLogger::init(&pc);
    ByzanceLogger::set_level(LOGGER_LEVEL_TRACE);
    ByzanceLogger::enable_prefix(false);
    pc.baud(115200);
}
```

Inicializační část, která je automaticky zavolána právě jednou po startu zařízení.

```cpp
void init(){
    pc.printf("Hello world\n");
}
```

Část kódu, který se bude točit stále dokola. Mezi každým loop\(\) se automaticky dává prostor i Byzance vláknu a \[\[feature:watchdog\|resetuje se watchdog\]\].

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
    pc.printf("Hello world\n");
}

void loop(){
    pc.printf("Test\n");
    Thread::wait(500);
}
```



