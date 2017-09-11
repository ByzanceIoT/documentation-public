# Command režim

## Příkazy bez parametru

* _''ping''_ - ping; pro testovací účely
* ''help'' - vypíše nápovědu do konzole
* ''overview'' - vypíše aktuální hodnotu všech parametrů, které jsou v bootloaderu nastavovat
* ''restart'' - restartuje Yodu. \[\[tutorial:restart\|Dokumentace k restartu\]\].
* ''target' -Typ desky. TODO: link
* ''fullid'' - vypíše FULL ID procesoru. \[\[hardware:full\_id\|Dokumentace\]\]. 
* ''trusted'' - Fuknce, která zjistí, jestli firmware je ověřený k běhu. \[\[feature:trusted\|Dokumentace k feature trusted\]\].
* ''launch\_reset'' - Pokud bylo předchozí spuštění firmware neúspěšné a není žádná validní binárka k obnovení, je třeba nahrát validní binárku a poté napsat příkaz ''launch\_reset''.
* ''defaults'' - Veškeré nastavení se obnoví do \[\[bootloader:defaults\|defaultních hodnot\]\].

###### Pokud zařízení používá DevList

* ''devlist\_clear'' - natvrdo smaže seznam všech uložených device v Yodovi. \[\[feature:devlist\|Dokumentace k devlist\]\].
* ''devlist\_counter'' - zjistí počet uložených device v Yodovi. \[\[feature:devlist\|Dokumentace k devlist\]\].
* ''devlist\_list'' - vypíše seznam všech uložených device v Yodovi. \[\[feature:devlist\|Dokumentace k devlist\]\].

## Příkazy s parametrem i bez

* ''normal\_mqtt\_hostname'' - Hlavní hostname, na kterém běží Homer. \[\[yoda:mqtt\|Dokumentace MQTT\]\].
* ''normal\_mqtt\_port'' -  Hlavní port, na kterém běží Homer. \[\[yoda:mqtt\|Dokumentace MQTT\]\].
* ''normal\_mqtt\_username'' - Hlavní jméno pro přihlášení k Homerovi. \[\[yoda:mqtt\|Dokumentace MQTT\]\].
* ''normal\_mqtt\_password'' - Hlavní heslo pro přihlášení k Homerovi. \[\[yoda:mqtt\|Dokumentace MQTT\]\].

* ''backup\_mqtt\_hostname'' - Záložní hostname, na kterém běží Homer. \[\[yoda:mqtt\|Dokumentace MQTT\]\].
* ''backup\_mqtt\_port'' - Záložní port, na kterém běží Homer. \[\[yoda:mqtt\|Dokumentace MQTT\]\].
* ''backup\_mqtt\_username'' - Záložní jméno pro přihlášení k Homerovi. \[\[yoda:mqtt\|Dokumentace MQTT\]\].
* ''backup\_mqtt\_password'' - Záložní heslo pro přihlášení k Homerovi. \[\[yoda:mqtt\|Dokumentace MQTT\]\].

* ''alias'' - Alias zařízení, který si každý může nastavit pro lepší rozpoznání zařízení. Více viz článek \[\[feature:alias\|alias\]\].
* ''mac'' - Zjištění MAC adresy. Souvisí s \[\[feature:ethernet\|ethernetem\]\].
* ''blreport - Bootloader report; zap nebo vyp textu do konzole, který píše \[\[bootloader:overview\|bootloader\]\].
* ''wdenable'' - Watchdog enable; zap nebo vyp \[\[feature:watchdog\|watchdogu\]\].
* ''wdtime'' - Nastavení periody resetu watchdogu \[\[feature:watchdog\|watchdogu\]\].
* ''autobackup'' - \[\[feature:autobackup\|Funkce, která zajišťuje, že při nahrátí nové binárky se stará zálohuje\]\].
* ''netsource'' - \[\[feature:netsource\|Zdroj internetu pro zařízení\]\].
* ''configured'' - při prvním spuštění bootloader naběhne vždy do Command režimu a čeká na konfiguraci všech parametrů. Až jsou parametry nastaveny, ''configured'' se přepne na 1 a tím se dá Yodovi najevo, že bude už nabíhat do normálního programu.
* ''timestamp'' - časové razítko pro obvod reálného času \(RTC\). Lze vyčíst funkcemi pro \[\[tutorial:timestamp\|práci s časem\]\].
* ''backuptime'' - Nastavení času, po kterém se spustí \[\[feature:autobackup\|automatická záloha firmware\]\]. 
* ''webview'' - Zapnutí nebo vypnutí \[\[tutorial:webview\|webového rozhraní\]\]
* ''webport'' - Port, na které poběží \[\[tutorial:webview\|webové rozhraní\]\]
* ''timeoffset'' - Slouží pro lokalizovanou \[\[tutorial:timestamp\|práci s časem\]\]. Nastavení offsetu lokálního času od UTC času.
* ''timesync'' - Slouží pro kontrolu synchronizace \[\[tutorial:timestamp\|času se servery\]\]. 
* ''lowpanbr'' - Zap nebo vyp funkce \[\[feature:lowpanbr\|lowpan border router\]\]
* ''restartbl'' - Identifikátor pro \[\[feature:restartbl\|restart zařízení do bootloaderu\]\]
* ''revision'' - Zjištění \[\[feature:revision\|revize zařízení\]\]

###### Pokud zařízení podporuje Wifi

* ''wifi\_ssid'' - Záložní jméno pro přihlášení k Homerovi. \[\[yoda:mqtt\|Dokumentace MQTT\]\].
* ''wifi\_password'' - Záložní heslo pro přihlášení k Homerovi. \[\[yoda:mqtt\|Dokumentace MQTT\]\].

## Příkazy pouze s parametrem

* ''info'' - Informace k dané komponentě. Parametry mohou být "bootloader", "firmware", "buffer", "backup".
* ''memsize' - Velikost oddílu, který je vyhrazen pro danou komponentu. Parametry mohou být "bootloader", "firmware", "buffer", "backup".
* ''intmem'' - Zformátuje paměť. Parametry mohou být "intmem" nebo "extmem". \[\[memory:internal\|Informace o interní paměti\]\].
* ''firmware' - Práce si firmwarem. Parametry mohou být "backup" pro zálohu, nebo "restore" pro obnovu.



