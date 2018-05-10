# Command mód

V command režimu je možné pomocí příkazů posílaných po sériové lince ověřovat a nastavovat konfigurační parametry.

Do command režimu bootloaderu je možno vstopit následujícím způsobem

1. podržet RESET a USER tlačítko dohromady
2. pustit RESET tlačítko
3. počkat několik sekund, než zhasne červená LED
4. pustit USER tlačítko

Při prvním spuštění nebo při položce configured=0 bootloader skáče do command režimu automaticky.

## Příkazy bez parametru

* **ping** - ping, pro testovací účely
* **help** - vypíše nápovědu do konzole
* **overview** - vypíše aktuální hodnotu všech parametrů, které jsou v bootloaderu nastaveny
* **restart** - restartuje Iodu. \[\[tutorial:restart\|Dokumentace k restartu\]\].
* **target** -Typ desky. TODO 
* **fullid** - vypíše FULL ID procesoru. [odkaz na fullid](https://github.com/byzance/public-documentation/tree/38b460c46404c197299c0f0a84e3402a9b74c8d7/byzance_documentation/architektura-fw/bootloader/TODO/README.md) 
* **launch\_reset** - Pokud bylo předchozí spuštění firmware neúspěšné a není žádná validní binárka k obnovení, je třeba nahrát validní binárku a poté napsat příkaz ''launch\_reset''.
* **defaults** - Veškeré nastavení se obnoví do [defaultního nastavení](https://github.com/byzance/public-documentation/tree/38b460c46404c197299c0f0a84e3402a9b74c8d7/byzance_documentation/architektura-fw/bootloader/TO%20DO%20ODKAZ/README.md).

## Příkazy s parametrem i bez

Více informací k MQTT připojení je možno nalézt v sekci [Komunikace se servery](../../konektivita/komunikace-s-portalem.md).

* **normal\_mqtt\_hostname** - Hostname, na kterém běží hlavní Homer.
* **normal\_mqtt\_port** -  Hlavní port, na kterém běží Homer.
* **backup\_mqtt\_hostname** - Záložní hostname, na kterém běží Homer.
* **backup\_mqtt\_port** - Záložní port, na kterém běží Homer. 
* **mqtt\_username** - Záložní jméno pro přihlášení k Homerovi.
* **backup\_mqtt\_password** - Záložní heslo pro přihlášení k Homerovi.
* **alias** - Alias zařízení, který si každý může nastavit pro lepší [identifikaci zařízení](../../funkcionality/identifikace-zarizeni.md).
* **mac** - Zjištění MAC adresy.
* **blreport** - Bootloader report. Zapnutí, nebo vypnutí výpisu hlavičky [bootloader](https://github.com/byzance/public-documentation/tree/38b460c46404c197299c0f0a84e3402a9b74c8d7/articles/hardware/ioda/navody/bootloader.md)u do konzole.
* **wdenable** - Zapnutí [watchdogu](../../funkcionality/watchdog.md).
* **wdtime** - Nastavení periody resetu [watchdogu](../../funkcionality/watchdog.md).
* **autobackup** - Funkce, která zajišťuje, že při nahrátí nové binárky se stará zálohuje.
* **netsource** - Zdroj, odkud bere zařízení internet.
* **configured** - při prvním spuštění bootloader naběhne vždy do Command režimu a čeká na konfiguraci všech parametrů. Až jsou parametry nastaveny, ''configured'' se přepne na 1 a tím se dá zařítzení najevo, že je již plně nakonfigurováno a příště bude už nabíhat do normálního programu.
* **webview** - Zapnutí nebo vypnutí \[\[tutorial:webview\|webového rozhraní\]\]
* **webport** - Port, na které poběží \[\[tutorial:webview\|webové rozhraní\]\]
* **timeoffset** - Slouží pro lokalizovanou \[\[tutorial:timestamp\|práci s časem\]\]. Nastavení offsetu lokálního času od UTC času.
* **timesync** - Slouží pro kontrolu synchronizace \[\[tutorial:timestamp\|času se servery\]\].
* **lowpanbr** - Zap nebo vyp funkce \[\[feature:lowpanbr\|lowpan border router\]\]
* **restartbl** - Identifikátor pro \[\[feature:restartbl\|restart zařízení do bootloaderu\]\]
* **revision** - Zjištění \[\[feature:revision\|revize zařízení\]\]

**Pokud zařízení podporuje Wifi**

* **wifi\_ssid** - Záložní jméno pro přihlášení k Homerovi. \[\[yoda:mqtt\|Dokumentace MQTT\]\].
* **wifi\_password** - Záložní heslo pro přihlášení k Homerovi. \[\[yoda:mqtt\|Dokumentace MQTT\]\].

## Příkazy pouze s parametrem

* **info** - Informace k dané komponentě.

  Parametry mohou být "bootloader", "firmware", "buffer", "backup".

* **memsize** - Velikost oddílu, který je vyhrazen pro danou komponentu.

  Parametry mohou být "bootloader", "firmware", "buffer", "backup".

* **intmem** - Zformátuje paměť.

  Parametry mohou být "intmem" nebo "extmem". \[\[memory:internal\|Informace o interní paměti\]\].

* **firmware** - Práce si firmwarem.

  Parametry mohou být "backup" pro zálohu, nebo "restore" pro obnovu.

