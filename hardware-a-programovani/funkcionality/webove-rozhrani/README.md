# Webové rozhraní

Webové rozhraní je funkce, která je součástí každého zařízení Byzance disponujícím Ethernetem. Slouží k zjištění, konfiguraci a monitorování základních funkcí a vlastností zařízení.

Pokud je zdrojem internetu 6lowpan či GSM, zařízení je schováno za NAT a webové rozhraní není dostupné. Možné zdroje internetu jsou dále vypsány v příslušné kapitole.

{% page-ref page="../../konektivita/specifikace-zdroje-internetu.md" %}

## Funkce webového rozhraní

* Zjištění [stavu firmware či probíhajících procedur na pozadí](spravce-firmware.md).
* Zjištění stavu[ softwarového restartu](zakladni-prehled.md).
* Zjištění verzí jednotlivých komponent firmware.
* [Využití výkonu](../vytizeni-zarizeni.md) mikrokontroléru a stav jednotlivých vláken.
* Výpis aktuálních hodnot [konfigurace](../../sprava-zarizeni/konfigurace-zarizeni.md), případně jejich změna.
* Zaregistrované Byzance [digitální/analogové/message vstupy a výstupy](../../programovani-hw/vstupy-a-vystupy-do-portalu.md).

## Jak získat přístup do webového rozhraní

Webové rozhraní musí být povoleno a nakonfigurováno na požadovaný port. K tomu je třeba zapnout proměnnou "webview" a nastavit "webport" libovolným způsobem konfigurace zařízení. Dále musí být nastaven "netsource" na "ethernet".

{% page-ref page="../../sprava-zarizeni/konfigurace-zarizeni.md" %}

V dalším kroku je třeba zjistit přidělenou IP adresu zařízení. Toho je možno docílit například při běhu firmware metodou get\_ip\_address\(\).

Jednoduchý kód pro vypisování IP adresy přes [sériovou linku](../../tutorialy/komunikace-po-seriove-lince-uart-s-pc/konfigurace-seriove-linky-v-pc.md) může vypadat následovně

```cpp
#include "byzance.h"

void init(){
	pc.baud(115200);
}

void loop(){
	printf("ip=%s\n", Byzance::get_ip_address());
	Thread::wait(1000);
}
```

Nakonec je třeba zadat nově zjištěnou IP adresu a případný port do webového prohlížeče. Pokud je port nastaven na standardních 80, není třeba jej zadávat. Je-li proměnná "webport" nastavena na cokoliv jiného \(například 1234\), je třeba port zadat do prohlížeče přes dvojtečku za přidělenou IP adresu.

Adresa i s portem pak může vypadat například následovně

> [http://192.168.67.4:1234/](http://192.168.67.4:1234/)

