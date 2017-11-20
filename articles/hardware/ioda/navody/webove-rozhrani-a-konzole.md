# Webové rozhraní

U Iody je možné využít webové rozhraní, pokud je povoleno v \[\[Bootloader:commands\| command režimu bootloaderu\]\]. Rozhraní slouží k zjištění a monitorování základních informací, hlavně z vývojářského hlediska.

### Nároky po zapnutí

* 1 vlákno
* 2kB stack RAM
* zhruba 2kB heap RAM
* 1 socket TCPSocket a 1 socket TCPServer
* několik KB flash paměti \(+- 10kB\), hlavně co se týče HTML kódu

### Jak se dostat do webového rozhraní

* webové rozhraní musí být povoleno \[\[Bootloader:commands\| v bootloaderu\]\] příkazy ''webview'' a nakonfigurováno na konrétní port příkazem ''webport''.
* Alternativně se dá nastavit pomocí příslušných MQTT topiců FIXME doplnit link
* je třeba zjistit IP adresu Yody \(například z routeru, nebo ze samotného programu \[\[tutorial:public\_functions\| metodou get\_ip\]\]
* zadat IP adresu do prohlížeče

### Funkce webového rozhraní

* Zjištění stavu firmware či \[\[tutorial:background\| probíhajících procedur na pozadí\]\]
* Zjištění stavu \[\[tutorial:restart\| softwarového restartu\]\]
* Zjištění verzí jednotlivých \[\[Yoda:aktualizace\_firmware\| komponent firmware\]\]
* Využití výkonu mikrokontroléru a stav jednotlivých vláken
* Výpis a nastavení všech \[\[Bootloader:commands\| proměnných z bootloaderu\]\]
* Seznam připojených zařízení FIXME nyní zastaralé
* Zaregistrované Byzance \[\[tutorial:byzance\_io\| digitální/analogové/message vstupy a výstupy viditelné z Blocka\]\]


### Vlákna na pozadí 

Výpis výtížení procesoru běžícími vlákny + obrázek z webového rozhraní 

 - TO DO -

### Ukázka webového rozhraní

![webview](/images/hardware/webview.png)


## Webová konzole 

Průběh vykonávání uživatelského programu je možné logovat pomocí webové konzole. Je implementována jako statická třída, funguje automaticky od začátku běhu programu a obsahuje následující veřejné metody dostupné uživateli.

```cpp
// zalogování erroru
static bool error(const char* format, ...);

// zalogování warningu
static bool warn(const char* format, ...);

// zalogování info
static bool info(const char* format, ...);

// zalogování logu
static bool log(const char* format, ...);

// je konzole aktivovaná?
static bool enabled();
```
### Vlastnosti konzole

Fukkce **error**, **warning**, **info** a **log** slouží k logování různých úrovní různých vlastních událostí, parametricky jsou shodné s C/C++ fukcí [[http://www.cplusplus.com/reference/cstdio/printf/| printf]]. Logy konzole se automaticky přenášejí do webového rozhraní Becki pomocí protokolu [[Yoda:MQTT|MQTT]], kde zařízení může uživatel sledovat. Návratovou hodnotou fukncí konzole je možné detekovat, jestli informace dorazila do webového rozhraní.

Fukce **enabled** slouží k zjištění, jestli je logování do webové konzole zapnuto. Logování se automaticky vypíná, pokud logy nikdo neodebírá. Je možné logy archivovat a odebírat, do budoucna asi za poplatek FIXME doplnit pak.

