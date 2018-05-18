# DevKitG3

Jedná se o vývojovou desku s integrovaným zařízením IODAG3E. Deska umožňuje:

* přímý přístup k X i Y konektoru
* vestavěný offline programátor
* vestavěný USB-UART převodník pro komunikaci po sériové lince
* tři uživatelská tlačítka
* tři uživatelské LED

![DevKitG3](../../../../.gitbook/assets/dkg3.png)

## Použití

Připojením DevKitu k PC je vytvořeno složené USB zařízení obsahující:

* mass storage zařízení \(flashdisk\) s názvem _BYZG3\_\*\*\*\*_
* virtuální sériový port

Aktualizace [firmware](../../../programovani-hw/struktura-programu.md) či [bootloaderu](../../../architektura-fw/bootloader/) IODA binárním souborem _\*.bin_ je možno provádět pomocí drag&drop z počítače na virtuální mass storage zařízení.

{% page-ref page="../../../programovani-hw/offline-programovani/upload-kodu-pomoci-zpp.md" %}

## Konektory

### USB

Konektor má několik funkcí:

* napájení přes USB
* vytváří složené zařízení pro Drag'n'Drop programování a virtuální sériový port

### Konektor X, Y

Rozložení pinů je stejné, jako na základní desce IODAG3E. Popis jednotlivých pinů je dostupný [v dokumentaci](../../zakladni-jednotky/iodag3e/konektor-x-a-y.md).

## Konfigurace

Jumperová propojka _JPL_ slouží k připojení uživatelských LED následujícím způsobem:

* Y12 - UL1 \(zelená\)
* Y13 - UL2 \(modrá\)
* Y14 - UL3 \(červená\)

Jumperová propojka _JPB_ slouží k připojení uživatelských tlačítek následujícím způsobem:

* UB1 - Y04
* UB2 - Y05
* UB3 - Y06

Jumperová propojka _JPP_ slouží k připojení programovací rozhraní a UART k zařízení IODA:

* DevKit/IODA SWCLK
* DevKit/IODA SWDIO
* DevKit/IODA nRST
* DevKit RX - IODA TX
* Devkit TX - IODA RX

Pro složitější operace je možno využívat [MSD příkazy](../../../programovani-hw/offline-programovani/upload-kodu-pomoci-zpp.md#msd-prikazy), či [aktualizovat firmware zařízení DAPlink](../../../programovani-hw/offline-programovani/upload-kodu-pomoci-zpp.md#aktualizace-firmware-programatoru).

## 

  


