# Command mód

Command mód je jeden z režimů [bootloaderu](./), kde je možné pomocí příkazů posílaných po [sériové lince](../../tutorialy/komunikace-po-seriove-lince-uart-s-pc/) ověřovat a [nastavovat konfigurační parametry](../konfigurace-zarizeni/). Ostatní režimy jsou popsány v [příslušné kapitole](rezimy-bootloaderu.md).

Do command režimu bootloaderu je možno vstopit následujícím způsobem

1. podržet RESET a USER tlačítko dohromady
2. pustit RESET tlačítko
3. počkat několik sekund, než zhasne žlutá LED
4. pustit USER tlačítko

![](../../../.gitbook/assets/bootloader.gif)

Při prvním spuštění nebo při položce configured=0 bootloader skáče do command režimu automaticky.

## Příkazy bez parametru

* **ping** - ping, pro testovací účely
* **help** - vypíše nápovědu do konzole
* **overview** - vypíše aktuální hodnotu všech parametrů, které jsou v bootloaderu nastaveny
* **restart** - restartuje zařízení.
* **target** -Typ desky. 
* **fullid** - vypíše FULL ID zařízení.  
* **launch\_reset** - Pokud bylo předchozí spuštění firmware neúspěšné a není žádná validní binárka k obnovení, je třeba nahrát validní binárku a poté napsat příkaz ''launch\_reset''.
* **defaults** - Veškeré nastavení se obnoví do [výchozích hodnot]().

## Příkazy s parametrem i bez

Více informací k MQTT připojení je možno nalézt v sekci [Komunikace se servery](../../konektivita/komunikace-s-portalem.md).

* **normal\_mqtt\_hostname** - Hostname, na kterém běží hlavní Homer.
* **normal\_mqtt\_port** -  Hlavní port, na kterém běží Homer.
* **backup\_mqtt\_hostname** - Záložní hostname, na kterém běží Homer.
* **backup\_mqtt\_port** - Záložní port, na kterém běží Homer. 
* **mqtt\_username** - Jméno pro přihlášení k Homerovi.
* **mqtt\_password** - Heslo pro přihlášení k Homerovi.
* **alias** - Alias zařízení, který si každý může nastavit pro lepší [identifikaci zařízení](../identifikace-zarizeni.md).
* **mac** - Zjištění MAC adresy.
* **blreport** - Bootloader report. Zapnutí, nebo vypnutí výpisu hlavičky [bootloaderu](./) do konzole.
* **wdenable** - Zapnutí [watchdogu](../../knowledge-base/watchdog.md).
* **wdtime** - Nastavení periody resetu [watchdogu](../../knowledge-base/watchdog.md).
* **autobackup** - Funkce, která zajišťuje, zajišťuje zálohu starého firmware při doručení nového.
* **netsource** - Zdroj, odkud bere zařízení internet.
* **configured** - při prvním spuštění bootloader naběhne vždy do Command režimu a čeká na konfiguraci všech parametrů. Až jsou parametry nastaveny, ''configured'' se přepne na 1 a tím se dá zařízení najevo, že je již plně nakonfigurováno a příště bude už nabíhat do normálního programu.
* **reconnect** - Nastavení, po kolika vteřinách se bude znovu provádět pokus o připojení k serveru v případě předchozího neúspěchu či odmítnutí.
* **encryption** - Zapnutí nebo vypnutí šifrování komunikace.
* **webview** - Zapnutí nebo vypnutí funkcionality [webového rozhraní](../webove-rozhrani/).
* **webport** - Port, na kterém bude přístupno [webové rozhraní](../webove-rozhrani/).
* **timeoffset** - Slouží pro lokalizovanou [práci s časem](../../tutorialy/datum-a-cas-rtc.md). Nastavení offsetu lokálního času RTC od UTC.
* **timesync** - Slouží pro zapnutí [synchronizace času](../../tutorialy/datum-a-cas-rtc.md) mezi servery Byzance a RTC.
* **lowpanbr** - Zapnutí funkce [lowpan border router](../../konektivita/6lowpan.md).
* **restartbl** - Identifikátor pro [restart zařízení do bootloaderu](./).
* **revision** - Zjištění [revize zařízení](command-mod.md)
* **autojump** - Nastavení časovače autojump na určitý čas. Po této době neaktivity \(v sekundách\) se zařízení přepne automaticky z bootloaderu do firmware.
* **lastpart** - zobrazuje počet části přijatých při posledním pokusu o aktualizaci bootloaderu firmwaru nebo backupu
* **confighash** - při změně nastavení se generuje nový confighash. Synchronizaci není nutno provádět vždy, ale pouze při změnách. Seznam parametrů, které generují nový confighash je možno nalézt v článku [omezení konfigurace](../omezeni-konfigurace/).

## Příkazy pouze s parametrem

* **info** - Informace k dané komponentě.

  Parametry mohou být "bootloader", "firmware", "buffer", "backup".

* **memsize** - Velikost oddílu, který je vyhrazen pro danou komponentu.

  Parametry mohou být "bootloader", "firmware", "buffer", "backup".

* **erase** - Zformátuje paměť.

  Parametry mohou být "firmware", "buffer", "backup", "extmem"

* **firmware** - Práce si firmwarem.

  Parametry mohou být "backup" pro zálohu, nebo "restore" pro obnovu.

