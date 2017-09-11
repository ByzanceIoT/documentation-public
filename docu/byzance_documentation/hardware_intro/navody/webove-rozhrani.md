# Webové rozhraní

U Yody je možné využít webové rozhraní, pokud je povoleno v \[\[Bootloader:commands\| command režimu bootloaderu\]\]. Rozhraní slouží k zjištění a monitorování základních informací, hlavně z vývojářského hlediska.

# Nároky po zapnutí

* 1 vlákno
* 2kB stack RAM
* zhruba 2kB heap RAM
* 1 socket TCPSocket a 1 socket TCPServer
* několik KB flash paměti \(+- 10kB\), hlavně co se týče HTML kódu

# Jak se dostat do webového rozhraní

* webové rozhraní musí být povoleno \[\[Bootloader:commands\| v bootloaderu\]\] příkazy ''webview'' a nakonfigurováno na konrétní port příkazem ''webport''.
* Alternativně se dá nastavit pomocí příslušných MQTT topiců FIXME doplnit link
* je třeba zjistit IP adresu Yody \(například z routeru, nebo ze samotného programu \[\[tutorial:public\_functions\| metodou get\_ip\]\]
* zadat IP adresu do prohlížeče

# Funkce webového rozhraní

* Zjištění stavu firmware či \[\[tutorial:background\| probíhajících procedur na pozadí\]\]
* Zjištění stavu \[\[tutorial:restart\| softwarového restartu\]\]
* Zjištění verzí jednotlivých \[\[Yoda:aktualizace\_firmware\| komponent firmware\]\]
* Využití výkonu mikrokontroléru a stav jednotlivých vláken
* Výpis a nastavení všech \[\[Bootloader:commands\| proměnných z bootloaderu\]\]
* Seznam připojených zařízení FIXME nyní zastaralé
* Zaregistrované Byzance \[\[tutorial:byzance\_io\| digitální/analogové/message vstupy a výstupy viditelné z Blocka\]\]

# Ukázka webového rozhraní



