# Ovládání LED modulu

LED modul je jedna ze základních součástí zařízení IODAG3E. Slouží k vizuální reprezentaci stavů. LED modul je automaticky řízen knihovnou Byzance.

{% page-ref page="../../funkcionality/led-modul.md" %}

Pokud je automatická signalizace řízená knihovnou z jakéhokoliv důvodu nevyhovující, je možno tuto funkcionalitu zakázat a nahradit vlastní.

K tomu slouží funkce [Byzance API](https://github.com/byzance/public-documentation/tree/38b460c46404c197299c0f0a84e3402a9b74c8d7/byzance_documentation/hardware_intro/API/byzance-api.md) příkaz ''led\_module\(false\)''. Pro případné opětovné zapnutí kontroly Byzance knihovnou stačí analogicky použít ''led\_module\(true\)''.

Dále je třeba inicializovat si LED modul dle vlastních potřeb. V závislosti na targetu je třeba zjistit typ LED modulu.

Pro RGB vypadá incializace takto

```cpp
DigitalOut ledRed(LED_RED);
DigitalOut ledGrn(LED_GREEN);
DigitalOut ledBlu(LED_BLUE);
```

Jednoduchý zdrojový kód může například následovný

```cpp
#include "byzance.h"

Serial    pc(SERIAL_TX, SERIAL_RX); // tx, rx

DigitalOut ledRed(LED_RED);
DigitalOut ledGreen(LED_GREEN);
DigitalOut ledBlue(LED_BLUE);

void init(){

    pc.baud(115200);
    pc.printf("LED Module test\n");

    // disable handling LED module from Byzance library
    Byzance::led_module(false);
}

void loop() {
    ledRed    = !ledRed;
    ledGreen    = !ledGreen;
    ledBlue    = !ledBlue;

    Thread::wait(1000);
}
```

Výše uvedený kód ve funkci init\(\) převezme kontrolu nad LED modulem a dále každou sekundu rozsvítí a posléze zhasne celý modul.

