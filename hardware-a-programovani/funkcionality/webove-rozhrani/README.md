# Webové rozhraní

Webové rozhraní je funkce, která je součástí každého zařízení Byzance a slouží k zjištění, konfiguraci a monitorování základních funkcí a vlastností zařízení.

## Funkce webového rozhraní

* Zjištění [stavu firmware či probíhajících procedur na pozadí](spravce-firmware.md).
* Zjištění stavu[ softwarového restartu](zakladni-prehled.md).
* Zjištění verzí jednotlivých komponent firmware.
* Využití výkonu mikrokontroléru a stav jednotlivých vláken.
* Výpis aktuálních hodnot konfigurace, případně jejich změna.
* Zaregistrované Byzance [digitální/analogové/message vstupy a výstupy](../../programovani-hw/vstupy-a-vystupy-do-portalu.md).

## Jak získat přístup do webového rozhraní

Webové rozhraní musí být povoleno a nakonfigurováno na požadovaný port. K tomu je třeba zapnout proměnnou "webview" a nastavit "webport" libovolným způsobem konfigurace zařízení.

{% page-ref page="../../uvod/konfigurace-zarizeni.md" %}

Je třeba zjistit IP adresu Iody. To je možno zjistit například z routeru \(ne vždy je to možné\), nebo při běhu firmware metodou get\_ip\_address\(\).

Jednoduchý kód pro vypisování IP adresy přes [sériovou linku](../../tutorialy/komunikace-po-seriove-lince-uart/konfigurace-pc.md) může vypadat následovně

```cpp
#include "byzance.h"

void init(){

	pc.baud(115200);

}

void loop(){

	to_computer("ip=%s\n", Byzance::get_ip_address());

	Thread::wait(1000);
}


```

Nakonec je třeba zadat IP adresu a případný port do webového prohlížeče. Pokud je port nastaven na standardních 80, není třeba jej zadávat. Je-li proměnná "webport" nastavena na cokoliv jiného \(například 1234\), je třeba port zadat do prohlížeče přes dvojtečku za přidělenou IP adresu.

Adresa i s portem pak může vypadat například následovně

> [http://192.168.67.4:1234/](http://192.168.67.4:1234/)

## Nároky po zapnutí

* 1 vlákno
* 2kB stack RAM
* zhruba 2kB heap RAM
* 1 socket TCPSocket a 1 socket TCPServer
* několik KB flash paměti \(+- 40kB\), převážně pro HTML kód

