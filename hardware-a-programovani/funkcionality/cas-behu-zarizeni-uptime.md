# Čas běhu zařízení \(Uptime\)

Uptime je čítač, který je implementovaný v každém zařízení Byzance. Vyjadřuje počet sekund uplynulých od zapnutí zařízení. Slouží především k monitoringu stability kódu a zjištění všeobecného přehledu o zařízení. Čítač se inkrementuje automaticky. Jeho maximální hodnota může být 2^32 - 1, tedy zhruba 136 let. Poté čítač přeteče znova na nulu.

Pokud je zařízení přepnuto do [bootloaderu](https://github.com/byzance/public-documentation/tree/38b460c46404c197299c0f0a84e3402a9b74c8d7/articles/hardware/ioda/navody/bootloader.md), ''Uptime'' se neinkrementuje.

## Jak zjistit hodnotu uptime

* Ve [webovém rozhraní](webove-rozhrani/)
* Pomocí uživatelského kódu a [Byzance API](../programovani-hw/byzance-hardware-api.md)

