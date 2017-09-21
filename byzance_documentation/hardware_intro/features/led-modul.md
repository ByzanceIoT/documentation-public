# LED modul

LED modul je součást každého Byzance zařízení. Slouží k signalizaci různých vnitřních stavů. Defaultní chování je řízeno [Byzance knihovnou](/byzance_documentation/hardware_intro/API/byzance-api.md), která se spouští automaticky po startu zařízení, či [bootloaderem](/byzance_documentation/hardware_intro/features/bootloader.md).

Automatický mód je popsán v článku[ LED signalizace](/byzance_documentation/hardware_intro/API/led-signalizace.md). Je možné však ale i převzít kontrolu nad LED modulem z uživatelského hlediska.

## Vlastní ovládání LED modulu

Nejdříve je třeba zakázat řízení LED modulu Byzance knihovnou. K tomu slouží funkce [Byzance API](/byzance_documentation/hardware_intro/API/byzance-api.md) ''led\_module\(false\)''. Pro případné opětovné zapnutí kontroly Byzance knihovnou stačí analogicky použít ''led\_module\(true\)''.

Dále je třeba inicializovat si LED modul dle vlastních potřeb. V závislosti na targetu je třeba zjistit typ LED modulu.

Pro RGB vypadá incializace takto

```cpp
DigitalOut ledRed(LED_RED);
DigitalOut ledGrn(LED_GREEN);
DigitalOut ledBlu(LED_BLUE);
```

Jednoduchý zdrojový kód může vypadat například takto

```cpp
#include "byzance.h"

Serial	pc(SERIAL_TX, SERIAL_RX); // tx, rx

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
    ledRed	= !ledRed;
    ledGreen	= !ledGreen;
    ledBlue	= !ledBlue;

    Thread::wait(1000);
}
```

Výše uvedený kód ve funkci init\(\) převezme kontrolu nad LED modulem a dále každou sekundu rozsvítí a posléze zhasne celý modul.



