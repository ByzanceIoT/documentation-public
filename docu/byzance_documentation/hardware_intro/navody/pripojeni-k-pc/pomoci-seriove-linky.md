# Připojení k PC pomocí sériové linky

Sériová linka je poměrně standardní rozhraní využívané v oblasti mikrokontrolérů. Pro připojení se využívá [MBED-OS API](/byzance_documentation/hardware_intro/API/mbed-api.md) pro [komunikační rozhraní](/byzance_documentation/hardware_intro/API/mbed-api/komunikacni-rozhrani.md). Pro správnou funkčnost je třeba sériovou komunikaci [zprovoznit ze strany počítače](/byzance_documentation/hardware_intro/navody/pripojeni-k-pc.md).

## Inicializace

Většina zařízení je vybavena více sériovými linkami, což je třeba specifikovat při inicializaci. Je nutné zjistit konkrétní piny, které disponují touto periferií. Tyto informace se dají zjistit v sekci [Hardware](/Hardware) vždy pro konkrétní zařízení.

V konstruktoru se zadávají parametry pinů TX a RX.

```cpp
Serial pc(SERIAL_TX, SERIAL_RX);
```

Dále je třeba zvolit baudovou rychlost. K tomu je vyhrazena sekce init\(\). Baudová rychlost může být různá, záleží na uživateli a pohybuje se většinou v rozmezí 1200 - 230400 baud. Stejnou rychlost je třeba nastavit [na straně počítače při připojení](/byzance_documentation/hardware_intro/navody/pripojeni-k-pc.md).

```cpp
pc.baud(115200);
```

## Ukázkový kód

Jednoduchý kód pro výpis ''hello word'' přes sériovou linku.

```cpp
#include "byzance.h"

Serial    pc(SERIAL_TX, SERIAL_RX);

void init(){
   pc.baud(115200);
}

void loop(){
   pc.printf("hello world\n");
   Thread::wait(500);
}
```



