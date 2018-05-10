# Programování sériové linky



Pro komunikaci po sériové lince s PC, nebo s libovolným dalším zařízením, je třeba vytvořit program, který sériovou linku inicializuje a dále bude odesílat a přijímat požadované zprávy. Zařízení IODA umožňuje incializovat sériovou linku dvěma způsoby, buď pomocí jeho [vývodů na konektoru XY](../../hardware/zakladni-jednotky/iodag3e/rozhrani-a-periferie.md), nebo pomocí emulátoru na konektoru microUSB.

## Komunikace pomocí Serial

Serial je konstruktor z knihovny [MBED API](../../programovani-hw/mbed-api/), který inicializuje Sériovou linku přímo na vývodech XY konektoru. Abychom mohli takto vytvořit linku mezi zařízením a PC, je potřeba využít TTL převodník, který  interpretuje komunikaci na USB. 

![P&#x159;ipojen&#xED; s&#xE9;riov&#xE9; linky pomoc&#xED; v&#xFD;vod&#x16F; XY konektoru](../../../.gitbook/assets/seriova_komunikace_ttl.png)

### Inicializace

V programu se nejprve sériová linka inicializuje pomocí třídy **Serial** z knihovny [MBED API](../../programovani-hw/mbed-api/). Argumenty konstruktoru jsou jména pinů **TX** a **RX**, na kterých se linka inicializuje.

```cpp
Serial pc(SERIAL_TX, SERIAL_RX);
```

Zařízení IODA umožňuje inicializovat několik sériových linek. Na kterých pinech se tyto linky dají inicializovat se lze dozvědět s dokumentace zařízení v sekci [Rozhraní a periférie](../../hardware/zakladni-jednotky/iodag3e/rozhrani-a-periferie.md) v oddíle UART/USART. V příkladu jsou místo jmen pinů použita makra **SERIALTX a SERIALRX**, tyto makra vedou na sériovou linku na pinech **Y00 a Y01.**

Dále je třeba zvolit baudovou rychlost, která určuje komunikační rychlost linky. To je nejvhodnější provést v sekci **init\(\)**. Baudová rychlost může být různá, záleží na uživateli a pohybuje se většinou v rozmezí 1200 - 230400 baud. Stejnou rychlost je třeba nastavit [na straně počítače při připojení](konfigurace-pc.md#konfigurace-na-windows).

```cpp
pc.baud(115200);
```

### Ukázkový kód

Jednoduchý kód pro výpis ''Hello word'' přes sériovou linku.

```cpp
#include "byzance.h"

Serial    pc(SERIAL_TX, SERIAL_RX);

void init(){
   pc.baud(115200);
}

void loop(){
   pc.printf("Hello world\n");
   Thread::wait(500);
}
```

## Komunikace pomocí USB

Zařízení IODA je dále schopné emulovat komunikaci po sériové lince přímo na konektoru microUSB tak ,aby nahradilo standardní sériovou linku a uživateli tak umožnilo komunikovat s PC bez nutnosti použít TTL převodník. Nevýhoda této komunikace je, že při každém restartu zařízení IODA je nutné zavřít a otevřít COM port, což prakticky znamená odpojit a znovu připojit sériový terminál.

![P&#x159;ipojen&#xED; s&#xE9;riov&#xE9; linky pomoc&#xED; microUSB](../../../.gitbook/assets/seriova_komunikace%20%282%29.png)

## Inicializace

Konstruktor USB linky může zůstat bez parametrů. V takovém případě se dosadí defaultní hodnoty. Nevýhodou může být to, že poslední parametr ''connect\_blocking'' je dosazen za ''true'', což znamená, že zařízení nepokračuje ve vykonávání kódu, dokud není připojeno USB a konstruktor je blokující. To může být v mnoha případech nežádoucí.

```cpp
USBSerial usb;
```

Vhodnější může být volba, aby USB konstruktor neblokoval kód, přičemž do parametrů konstruktoru je nutné připsat i produktové kódy zařízení. Konstruktor bude mít poté podobu. 

```cpp
USBSerial usb(0x1f00, 0x2012, 0x0001, false);
```

V případě USB se narozdíl od sériové linky **nenastavuje baudová rychlost**.

## Ukázkový kód

Velmi jednoduchý kód pro výpis ''hello world'' pomocí USB může vypadat například takto

```cpp
USBSerial usb(0x1f00, 0x2012, 0x0001, false);

void loop(){
   usb.printf("hello world\n");
   Thread::wait(500);
}
```

