# Konfigurace zařízení

## Základní informace

Všechna zařízení IODAG3E jsou konfigurovatelná .

## Konfigurace z Portálu

pokec

![](../../.gitbook/assets/config_portal.PNG)

## Konfigurace pomocí bootloaderu

[Bootloader ](../architektura-fw/bootloader/)je firmwarová komponenta \(zavaděč\). Spouští se jako první po startu zařízení a rozhoduje o tom, jestli dojde ke spuštění firmware, nebo vykoná některou se svých dalších možných funkcí. Jednou z těchto z těchto funkcí je [command režim](../architektura-fw/bootloader/command-mod.md), sloužící ke konfiguraci zařízení, pokud je offline. 

Konfigurace probíhá pomocí [sériové linky](../tutorialy/komunikace-po-seriove-lince-uart/#konfigurace-pc). Dojde-li ke konfliktu mezi nastavením provedeným z Bootloaderu a z Portálu, přednost má Portál a lokální nastavení v IODA je přepsáno. 

## Konfigurace z Byzance API

pokec

## Konfigurace z webového rozhraní



