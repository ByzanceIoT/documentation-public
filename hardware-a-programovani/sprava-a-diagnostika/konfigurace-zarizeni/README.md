# Konfigurace zařízení

## Základní informace

Všechna zařízení IODAG3E jsou konfigurovatelná. Před každou změnou výchozí konfigurace je třeba chápat synchronizační mechanismus vůči serveru a uvědomit si možné důsledky. Konfigurační parametry totiž existují na dvou místech - online v Cloudu a offline v IODAG3E.

Dojde-li ke konfliktu mezi jednotlivými konfiguračními soubory, soubor v IODAG3E je při připojení k Portálu automaticky přepsán konfigurací z Portálu. Proto je nutno konfiguraci provádět primárně přes Portál. Ostatní metody je třeba brát jako doplňkové pro případ, že bude zařízení offline.

Každá změna konfigurace generuje nový [confighash](confighash.md). Jedná se o speciální položku, která umožňuje přeskakování synchronizace, pokud se nic nezměnilo mezi odpojením od serverů a opětovném připojení.

Výchozí hodnoty konfigurace, výjimky nereagující na confighash a možná omezení jsou popsány v článku [Omezení konfigurace](../omezeni-konfigurace/).

![](../../../.gitbook/assets/local-global-config-file.jpg)

## Konfigurace z Portálu

Preferovaný způsob při změně konfigurace. Přehled jednotlivých parametrů je možno nalézt v online Portálu v možnostech daného zařízení, záložka Developer Settings.

![](../../../.gitbook/assets/config_portal.PNG)

## Konfigurace pomocí bootloaderu

[Bootloader ](../bootloader/)je firmwarová komponenta \(zavaděč\). Spouští se jako první po startu zařízení a rozhoduje o tom, jestli dojde ke spuštění firmware, nebo vykoná některou se svých dalších možných funkcí. Jednou z těchto z těchto funkcí je [command režim](../bootloader/command-mod.md), sloužící ke konfiguraci zařízení - především pokud je offline.

Konfigurace probíhá pomocí [sériové linky](../../tutorialy/komunikace-po-seriove-lince-uart-s-pc/#konfigurace-pc). Dojde-li ke konfliktu mezi nastavením provedeným z Bootloaderu a z Portálu, přednost má Portál a lokální nastavení v IODA je přepsáno.

{% page-ref page="../bootloader/" %}

## Konfigurace z Byzance API

Pro zjištění či nastavení jednotlivých konfiguračních parametrů v průběhu běhu firmware je možno využít [Byzance API](../../programovani-hw/byzance-api/).

Příklad pro zjištění např. položky "Alias" může vypadat takto

```cpp
#include "byzance.h"

char alias[64];

void init(){

    Byzance::get_alias(alias);
    printf("alias: %s\n", alias);

}

void loop(){

    Thread::wait(500);

}
```

Stejně jako v ostatních případech, pokud dojde ke změně konfiguračních parametrů pomocí [Byzance API](../../programovani-hw/byzance-api/) přímo v zařízení, parametry mohou být po připojení k internetu IODAG3E přepsány konfigurací z Portálu.

{% page-ref page="../../programovani-hw/byzance-api/" %}

## Konfigurace z webového rozhraní

[Webové rozhraní](../webove-rozhrani/) IODAG3E \(webview\) je služba, která vznikla za účelem jednodušší kontroly zařízení, monitoringu a správu firmware. Pokud je webové rozhraní zapnuto a uživatel je i s IODAG3E na stejné síti \(platí pouze pro Ethernet\), je možné navštívit příslušnou URL požadovaného zařízení.

Nutno brát v potaz, že lokálně provedené změny na IODAG3E mohou být přepsány Portálem při dalším připojení.

{% page-ref page="../webove-rozhrani/" %}

