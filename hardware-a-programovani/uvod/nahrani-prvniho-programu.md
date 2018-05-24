---
description: '#todo dát někam do piče'
---

# Nahrání prvního programu

## Jak vytvořit první program?

Hardware Byzance se programuje v jazyce C++ a k programování má dostupné všechny standartní knihovny, knihovny [Mbed API](../programovani-hw/mbed-api/) a [Byzance Hardware API](../programovani-hw/byzance-api/)**.** Jak má vypadat tělo programje možno se dozvědět v sekci [Struktura programu](../programovani-hw/struktura-programu.md). Každý program musí obsahovat alespoň jeden hlavní soubor **main.cpp**, jinak se kompilace neprovede správně.

Vhodnou ukázkou prvního programu může být například známý **Hello World**, který pravidelně vypisuje pozdrav přes [sériovou linku](../tutorialy/komunikace-po-seriove-lince-uart-s-pc/#konfigurace-pc).

```cpp
#include "byzance.h"

USBSerial usb(0x1f00, 0x2012, 0x0001, false);

void init(){
    // Hello world se vypise jednou pri startu
    usb.printf("Hello world from init function\n");
}

void loop(){
    // Hello world se bude vypisovat stale dokola kazdych 500 ms
    usb.printf("Hello World\n");
    Thread::wait(500);
}
```

## Jak zkompilovat první program?

Předtím, než je možné do zařízení program nahrát a spustit, je potřeba ho nejprve zkompilovat a vytvořit tak strojově čitelný binární kód. To je možné provést přímo v PC ručně, kdy si nejprve musíme nakonfigurovat potřebné knihovny viz sekci [Offline programování](../programovani-hw/offline-programovani/), nebo použijeme portál, kde lze program zkompilovat online viz Kompilace programu v portálu \( \#TODO odkaz na článek viz ticket [BECKI-408](https://youtrack.byzance.cz/youtrack/issue/BECKI-408)\)

## Jak nahrát program do zařízení?

Upload programu z portálu \( \#TODO odkaz na článek viz ticket [BECKI-409](https://youtrack.byzance.cz/youtrack/issue/BECKI-409)\).

Offline programování programátorem ST-LINK či pomocí drag&drop je dále popsáno v příslušné kapitole.

{% page-ref page="../programovani-hw/offline-programovani/" %}

