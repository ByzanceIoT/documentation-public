# Provozní informace

## Čas běhu zařízení

Čas běhu zařízení, neboli "uptime" je čítač, který je implementovaný v každém zařízení Byzance. Vyjadřuje počet sekund uplynulých od zapnutí zařízení. Slouží především k monitoringu stability kódu a zlepšení všeobecného přehledu o zařízení. Čítač se inkrementuje automaticky. Jeho maximální hodnota může být 2^32 - 1, tedy zhruba 136 let. Poté čítač přeteče znova na nulu.

Pokud je zařízení přepnuto do [bootloaderu](../architektura-fw/bootloader/), ''uptime'' se neinkrementuje.

Hodnotu uptime je možno zjistit

* Ve [webovém rozhraní](webove-rozhrani/)
* Pomocí uživatelského kódu a [Byzance API](../programovani-hw/byzance-hardware-api.md)

## Čas připojení k serverům

Je-li zařízení připojeno k internetu, je možno zjistit, jak dlouho od startu je připojeno k serverům. Tato položka je pojmenována "connected time". Čítač je podobně jako "uptime" implementován jako 32 bitové číslo, které se automaticky inkrementuje každou sekundu. Jeho maximální hodnota může být 2^32 - 1, tedy zhruba 136 let. Poté čítač přeteče znova na nulu.

Při každém odpojení od serverů se čítač přestane inkrementovat a resetuje se do nuly.

Hodnotu "connected time" je možno zjistit

* Ve [webovém rozhraní](webove-rozhrani/)
* Pomocí uživatelského kódu a [Byzance API](../programovani-hw/byzance-hardware-api.md)

## Napájecí napětí

bla

\#TODO: referencovat potom na napájení iody

## Referenční napětí

bla



## Teplota jádra

R

| Rozsah teplot | -40°C až 125°C |
| --- | --- |
| Přesnost | ± 1,5°C |

## 



