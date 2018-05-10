# Programování sériové linky



Zde bude návod

* Jak zapojit sériovou linku \(stručně schéma s grafikou IODY! a stručně vysvětlit nebo odkázat někam kde je vysvětleno \)
* Vysvětlit makra SERIAL TX, SERIAL\_RX a jejich použití při komunikaci přes microUSB !! Vysvětlit, že pokud inicializuji jinou sériovou linku někde na pinech \(Krom Y00 a Y01\) tak nebude fungovat
* Krátký stručný kód



Pro komunikaci po sériové lince s PC, nebo s libovolným dalším zařízením, je třeba vytvořit program, který sériovou linku inicializuje a dále bude odesílat a přijímat požadované zprávy. Zařízení IODA umožňuje incializovat sériovou linku dvěma způsoby, buď pomocí jeho [vývodů na konektoru XY](../../hardware/zakladni-jednotky/iodag3e/rozhrani-a-periferie.md).

## Komunikace pomocí Serial

Serial je konstruktor z knihovny [MBED API](../../programovani-hw/mbed-api/), který inicializuje Sériovou linku přímo na vývodech XY konektoru. Abychom mohli takto vytvořit linku mezi zařízením a PC, je potřeba využít TTL převodník, který  interpretuje komunikaci na USB. 

![P&#x159;ipojen&#xED; s&#xE9;riov&#xE9; linky pomoc&#xED; v&#xFD;vod&#x16F; XY konektoru](../../../.gitbook/assets/seriova_komunikace_ttl.png)

### Inicializace

V programu se nejprve sériová linka inicializuje pomocí třídy **Serial** z knihovny [MBED API](../../programovani-hw/mbed-api/). Argumenty konstruktoru jsou jména pinů **TX** a **RX**, na kterých se linka inicializuje.

```cpp
Serial pc(SERIAL_TX, SERIAL_RX);
```

Zařízení IODA umožňuje inicializovat několik sériových linek. Na kterých pinech se tyto linky dají inicializovat se lze dozvědět s dokumentace zařízení v sekci [Rozhraní a periférie](../../hardware/zakladni-jednotky/iodag3e/rozhrani-a-periferie.md) v oddíle UART/USART. V příkladu jsou místo jmen pinů použita makra **SERIALTX a SERIALRX**, tyto makra vedou na sériovou linku na pinech **Y00 a Y01.**



Dále je třeba zvolit baudovou rychlost. K tomu je vyhrazena sekce init\(\). Baudová rychlost může být různá, záleží na uživateli a pohybuje se většinou v rozmezí 1200 - 230400 baud. Stejnou rychlost je třeba nastavit [na straně počítače při připojení](https://github.com/byzance/public-documentation/tree/38b460c46404c197299c0f0a84e3402a9b74c8d7/byzance_documentation/hardware_intro/navody/pripojeni-k-pc.md).

```cpp
pc.baud(115200);
```

### Ukázkový kód

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

## Komunikace pomocí USB

Některá Byzance zařízení je možné připojit pomocí USB. USB je koncipováno především k tomu, aby nahradilo standardní sériovou linku, čímž odpadne nutnost použití převodníku s FTDI čipem. Všeobecné informace, jak zprovoznit komunikaci ze strany počítače jsou popsány v článku [Připojení k PC](https://github.com/byzance/public-documentation/tree/38b460c46404c197299c0f0a84e3402a9b74c8d7/byzance_documentation/hardware_intro/navody/pripojeni-k-pc.md). Nevýhoda je taková, že při každém restartu zařízení se USB odpojí a připojí k počítači a je třeba v ovládací aplikaci znovu otevřít COM port.

![P&#x159;ipojen&#xED; s&#xE9;riov&#xE9; linky pomoc&#xED; microUSB](../../../.gitbook/assets/seriova_komunikace%20%282%29.png)

## Inicializace

Konstruktor USB linky může zůstat bez parametrů. V takovém případě se dosadí defaultní hodnoty. Nevýhodou může být to, že poslední parametr ''connect\_blocking'' je dosazen za ''true'', což znamená, že zařízení nepokračuje ve vykonávání kódu, dokud není připojeno USB a konstruktor je blokující. To může být v mnoha případech nežádoucí.

```cpp
USBSerial usb;
```

Vhodnější může být volba, aby USB konstruktor neblokoval kód, přičemž produktové kódy se musí dosadit do předchozích parametrů.

```cpp
USBSerial usb(0x1f00, 0x2012, 0x0001, false);
```

V případě USB se narozdíl od sériové linky nenastavuje baudová rychlost.

## Ukázkový kód

Velmi jednoduchý kód pro výpis ''hello world'' pomocí USB může vypadat například takto

```cpp
USBSerial usb;

void loop(){
   usb.printf("hello world\n");
   Thread::wait(500);
}
```

