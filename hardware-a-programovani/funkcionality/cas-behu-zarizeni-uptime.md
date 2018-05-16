# Provozní informace

## Uptime

Uptime je čítač, který je implementovaný v každém zařízení Byzance. Vyjadřuje počet sekund uplynulých od zapnutí zařízení. Slouží především k monitoringu stability kódu a zjištění všeobecného přehledu o zařízení. Čítač se inkrementuje automaticky. Jeho maximální hodnota může být 2^32 - 1, tedy zhruba 136 let. Poté čítač přeteče znova na nulu.

Pokud je zařízení přepnuto do [bootloaderu](../architektura-fw/bootloader/), ''Uptime'' se neinkrementuje.

```text
uptime kód
```

## Jak zjistit hodnotu uptime

* Ve [webovém rozhraní](webove-rozhrani/)
* Pomocí uživatelského kódu a [Byzance API](../programovani-hw/byzance-hardware-api.md)

## Connected time



