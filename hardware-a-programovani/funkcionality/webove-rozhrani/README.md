# Webové rozhraní

Webové rozhraní je funkce, která je součástí každého zařízení Byzance a slouží k zjištění, konfiguraci a monitorování základních funkcí a vlastností zařízení.

## Funkce webového rozhraní

* Zjištění stavu firmware či probíhajících procedur na pozadí.
* Zjištění stavu softwarového restartu.
* Zjištění verzí jednotlivých komponent firmware.
* Využití výkonu mikrokontroléru a stav jednotlivých vláken.
* Výpis aktuálních hodnot konfigurace, případně změna.
* Zaregistrované Byzance digitální/analogové/message vstupy a výstupy.

## Jak získat přístup do webového rozhraní

* Webové rozhraní musí být povoleno v [bootloaderu příkazy](../../architektura-fw/bootloader/) ''webview=1'' a nakonfigurováno na konrétní port příkazem ''webport''=80.
* Je třeba zjistit IP adresu Iody \(například z routeru, nebo při běhu firmware metodou get\_ip\).
* Nakonec je třeba zadat IP adresu a případný port do webového prohlížeče.

## Nároky po zapnutí

* 1 vlákno
* 2kB stack RAM
* zhruba 2kB heap RAM
* 1 socket TCPSocket a 1 socket TCPServer
* několik KB flash paměti \(+- 40kB\), převážně pro HTML kód

