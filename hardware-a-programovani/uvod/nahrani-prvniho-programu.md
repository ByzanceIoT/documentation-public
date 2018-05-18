# Nahrání prvního programu

## Jak vytvořit první program? 

Hardware Byzance se programuje v jazyce C++ a k programování má dostupné všechny standartní knihovny, knihovny [Mbed API](../programovani-hw/mbed-api/) a [Byzance Hardware API](../programovani-hw/byzance-hardware-api/)**.** Jak má vypadat tělo programje možno se dozvědět v sekci [Struktura programu](../programovani-hw/struktura-programu.md). Každý program musí obsahovat alespoň jeden hlavní soubor **main.cpp**, jinak se kompilace neprovede správně. 

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

Předtím, než je možné do zařízení program nahrát a spustit, je potřeba ho nejprve zkompilovat a vytvořit tak strojově čitelný binární kód. To je možné provést přímo v PC ručně, kdy si nejprve musíme nakonfigurovat potřebné knihovny viz sekci [Offline programování](../programovani-hw/offline-programovani/), nebo použijeme portál, kde lze program zkompilovat online viz Kompilace programu v portálu \( \#TODO odkaz na článek viz ticket  [BECKI-408](https://youtrack.byzance.cz/youtrack/issue/BECKI-408)\)

## Jak nahrát program do zařízení?

Poté co získáme zkompilovaný program v binárním podobě,  můžeme kód  nahrát do zařízení. Pokud obsluhujeme zařízení přes portál,  postupujeme podle návodu Upload programu z portálu \( \#TODO odkaz na článek viz ticket  [BECKI-409](https://youtrack.byzance.cz/youtrack/issue/BECKI-409)\). 

Pokud nahráváme program do zařízení přímo z PC , máme několik možností jak to provést. 

### Programování pomocí ZPP

K programování můžeme použít zařízení [Byzance ZPPG3](../hardware/ostatni/zppg3/), které umožňuje drag&drop programování. Toto zařízení připojíme k programovacímu konektoru a PC a zařízení IODA zapojíme do napájení.  V počítači se hned poté inicializuje nový flash disk, na který stačí binární kód vložit a automaticky se nahraje do zařízení.

 \#TODO \(GIF pripojení ZPP do počítače a IODY - ticket  [HW-1054](https://youtrack.byzance.cz/youtrack/issue/HW-1054)\)

Podrobný návod programování pomocí ZPP lze nalézt v sekci [Upload kódu pomocí ZPP](../programovani-hw/offline-programovani/upload-kodu-pomoci-zpp.md). 

### Programování zařízení DevKit

Zařízení DevKit, má v sobě programátor zabudovaný, tudíž není nutné k programování využívat žádné další zařízení. DevKit stačí připojit k PC usb kabelem a v počítači se inicializuje nový flash disk, na který stačí binární kód přetáhnout drag&drop stejně jako pomocí ZPP.

### Programování pomocí programátoru ST-link

Vzhledem k tomu, že zařízení IODAG3E  má integrovaný procesor STM, je možné ho programovat pomocí programátoru ST-link. Pro více informací pokračujte do sekce [Upload kódu z GUI](../programovani-hw/offline-programovani/upload-kodu-z-gui.md). 

















