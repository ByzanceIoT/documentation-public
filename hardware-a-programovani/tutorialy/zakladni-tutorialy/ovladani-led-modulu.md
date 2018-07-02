# Ovládání LED modulu

LED modul je jedna ze základních součástí zařízení IODAG3E. Slouží k vizuální reprezentaci stavů. LED modul je automaticky řízen knihovnou Byzance.

![](../../../.gitbook/assets/assets-2f-l9jhrot0uirgp5ehgdl-2f-lbewd4wspeqb5newn6p-2f-lbewhzmwxh3tbwhkxwu-2fdisconnected%20%281%29.gif)

{% page-ref page="../../sprava-a-diagnostika/led-modul.md" %}

Pokud je automatická signalizace řízená knihovnou z jakéhokoliv důvodu nevyhovující, je možno tuto funkcionalitu zakázat a nahradit vlastní.

K tomu slouží funkce [Byzance API](../../programovani-hw/byzance-api/) příkaz `led_module(false)`. Pro případné opětovné zapnutí kontroly Byzance knihovnou stačí analogicky použít `led_module(true)`.

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

