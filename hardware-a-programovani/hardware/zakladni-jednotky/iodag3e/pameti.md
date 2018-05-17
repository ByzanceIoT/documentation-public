# Paměti

## Přehled

Jednotka IODAG3E obsahuje několik druhů pamětí, kde každý typ má svůj účel a svá specifika. Jedná se o volatilní paměť RAM a nevolatilní paměť FLASH integrovanou v pouzdře mikrokontroléru a o větší externí FLASH paměť.

* RAM
  * 256 kB SRAM \(včetně 64 kB CCM\)
  * 4 kB zálohované SRAM \(zálohováno [_VBAT_ ](../../../funkcionality/pripojeni-zdroje-k-vbat.md)zdrojem\) 
  * součást mikrokontroléru sloužící pro data běžícího firmware
* FLASH
  * 2 MB v mikrokontroléru
  * rozděleno na stránky o různých velikostech
  * slouží pro firmware a bootloader jednotky
* externí FLASH
  * velikost 64 Mb
  * připojena přes SPI rozhraní k mikrokontroléru
  * slouží pro uložení konfigurace, záložního firmware a jako uživatelský prostor

## FLASH v mikrokontroléru

### Rozdělení sektorů

Většina mikrokontrolérů Cortex M4 má banky paměti rozdělené do menších částí, tzv. sektory. Platí to i pro mikrokontrolér použitý v jednotce IODAG3E a sektory jsou rozděleny podle tabulky níže. V případě použitého mikrokontroléru je paměť složena z více paměťových bank \(dvě banky po 1 MB\), struktura rozdělení sektorů se u druhé banky opakuje.

| **Sektor číslo** | **Velikost sektoru \[kB\]** | **Počáteční adresy** |
| --- | --- | --- | --- | --- | --- | --- |
| 0 až 3 | 16 | 0x8000000 |
| 4 | 64 |  |
| 5 až 11 | 128 |  |
| 12 až 15 | 16 |  |
| 16 | 64 |  |
| 17 až 23 | 128 |  |

### Důsledky existence sektorů

Vzhledem k rozdělení paměti a existenci bootloaderu a hlavního programu je FLASH paměť logicky rozdělena na dvě části.

* bootloader 64 kB - od adresy 0x08000000 po 0x80010000, sektory 0 až  3
* firmware 1984 kB - od adresy 0x8010000 po 0x80200000,  - sektory 4 až 23

Adresy 0x08000000 a 0x08010000 je tedy třeba znát při [ručním nahrávání](../../../programovani-hw/offline-programovani/) bootloaderu nebo firmware \(např přes [ST-LINK](../../../programovani-hw/offline-programovani/upload-kodu-z-gui.md)\).

### Přímá uživatelská práce s interní FLASH

Přímá uživatelská práce s interní FLASH pamětí mikrokontroléru se nedoporučuje, protože může dojít k poškození firmware nebo bootloaderu. Výše uvedené skutečnosti je třeba reflektovat \(především při mazání, kde se může stát, že je třeba smazat jenom několik bytů dat, ale technologie FLASH smaže celou stránku společně i s jinými daty\).



