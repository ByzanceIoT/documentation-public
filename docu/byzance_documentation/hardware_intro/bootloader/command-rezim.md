# Command režim

## Příkazy bez parametruit

* _''ping''_ - ping; pro testovací účely
* ''_help_'' - vypíše nápovědu do konzole
* ''_overview_'' - vypíše aktuální hodnotu všech parametrů, které jsou v bootloaderu nastavovat
* ''_restart_'' - restartuje Yodu. \[\[tutorial:restart\|Dokumentace k restartu\]\].
* ''_target_' -Typ desky. TODO: link
* ''_fullid_'' - vypíše FULL ID procesoru. \[\[hardware:full\_id\|Dokumentace\]\]. 
* ''_trusted_'' - Fuknce, která zjistí, jestli firmware je ověřený k běhu. \[\[feature:trusted\|Dokumentace k feature trusted\]\].
* ''_launch\_reset_'' - Pokud bylo předchozí spuštění firmware neúspěšné a není žádná validní binárka k obnovení, je třeba nahrát validní binárku a poté napsat příkaz ''launch\_reset''.
* ''_defaults_'' - Veškeré nastavení se obnoví do \[\[bootloader:defaults\|defaultních hodnot\]\].

**Pokud zařízení používá DevList**

* ''_devlist\_clear_'' - natvrdo smaže seznam všech uložených device v Yodovi. \[\[feature:devlist\|Dokumentace k devlist\]\].
* ''_devlist\_counter_'' - zjistí počet uložených device v Yodovi. \[\[feature:devlist\|Dokumentace k devlist\]\].
* ''_devlist\_list_'' - vypíše seznam všech uložených device v Yodovi. \[\[feature:devlist\|Dokumentace k devlist\]\].

## Příkazy s parametrem i bez

* ''_normal\_mqtt\_hostname_'' - Hlavní hostname, na kterém běží Homer. \[\[yoda:mqtt\|Dokumentace MQTT\]\].
* ''_normal\_mqtt\_port_'' -  Hlavní port, na kterém běží Homer. \[\[yoda:mqtt\|Dokumentace MQTT\]\].
* ''_normal\_mqtt\_username_'' - Hlavní jméno pro přihlášení k Homerovi. \[\[yoda:mqtt\|Dokumentace MQTT\]\].
* ''_normal\_mqtt\_password_'' - Hlavní heslo pro přihlášení k Homerovi. \[\[yoda:mqtt\|Dokumentace MQTT\]\].

* ''_backup\_mqtt\_hostname_'' - Záložní hostname, na kterém běží Homer. \[\[yoda:mqtt\|Dokumentace MQTT\]\].

* ''_backup\_mqtt\_port_'' - Záložní port, na kterém běží Homer. \[\[yoda:mqtt\|Dokumentace MQTT\]\].

* ''_backup\_mqtt\_username_'' - Záložní jméno pro přihlášení k Homerovi. \[\[yoda:mqtt\|Dokumentace MQTT\]\].
* ''_backup\_mqtt\_password_'' - Záložní heslo pro přihlášení k Homerovi. \[\[yoda:mqtt\|Dokumentace MQTT\]\].

* ''_alias_'' - Alias zařízení, který si každý může nastavit pro lepší rozpoznání zařízení. Více viz článek \[\[feature:alias\|alias\]\].

* ''_mac_'' - Zjištění MAC adresy. Souvisí s \[\[feature:ethernet\|ethernetem\]\].

* ''_blreport _- Bootloader report; zap nebo vyp textu do konzole, který píše \[\[bootloader:overview\|bootloader\]\].

* ''_wdenable_'' - Watchdog enable; zap nebo vyp \[\[feature:watchdog\|watchdogu\]\].

* ''_wdtime_'' - Nastavení periody resetu watchdogu \[\[feature:watchdog\|watchdogu\]\].

* ''_autobackup_'' - \[\[feature:autobackup\|Funkce, která zajišťuje, že při nahrátí nové binárky se stará zálohuje\]\].

* ''_netsource_'' - \[\[feature:netsource\|Zdroj internetu pro zařízení\]\].

* ''_configured_'' - při prvním spuštění bootloader naběhne vždy do Command režimu a čeká na konfiguraci všech parametrů. Až jsou parametry nastaveny, ''configured'' se přepne na 1 a tím se dá Yodovi najevo, že bude už nabíhat do normálního programu.
* ''_timestamp_'' - časové razítko pro obvod reálného času \(RTC\). Lze vyčíst funkcemi pro \[\[tutorial:timestamp\|práci s časem\]\].
* ''_backuptime_'' - Nastavení času, po kterém se spustí \[\[feature:autobackup\|automatická záloha firmware\]\]. 
* ''_webview_'' - Zapnutí nebo vypnutí \[\[tutorial:webview\|webového rozhraní\]\]
* ''_webport_'' - Port, na které poběží \[\[tutorial:webview\|webové rozhraní\]\]
* ''_timeoffset_'' - Slouží pro lokalizovanou \[\[tutorial:timestamp\|práci s časem\]\]. Nastavení offsetu lokálního času od UTC času.
* ''_timesync_'' - Slouží pro kontrolu synchronizace \[\[tutorial:timestamp\|času se servery\]\]. 
* ''_lowpanbr_'' - Zap nebo vyp funkce \[\[feature:lowpanbr\|lowpan border router\]\]
* ''_restartbl_'' - Identifikátor pro \[\[feature:restartbl\|restart zařízení do bootloaderu\]\]
* ''_revision_'' - Zjištění \[\[feature:revision\|revize zařízení\]\]

**Pokud zařízení podporuje Wifi**

* ''_wifi\_ssid_'' - Záložní jméno pro přihlášení k Homerovi. \[\[yoda:mqtt\|Dokumentace MQTT\]\].
* ''_wifi\_password_'' - Záložní heslo pro přihlášení k Homerovi. \[\[yoda:mqtt\|Dokumentace MQTT\]\].

## Příkazy pouze s parametrem

* ''_info_'' - Informace k dané komponentě. Parametry mohou být "bootloader", "firmware", "buffer", "backup".
* ''_memsize_' - Velikost oddílu, který je vyhrazen pro danou komponentu. Parametry mohou být "bootloader", "firmware", "buffer", "backup".
* ''_intmem_'' - Zformátuje paměť. Parametry mohou být "intmem" nebo "extmem". \[\[memory:internal\|Informace o interní paměti\]\].
* ''_firmware_' - Práce si firmwarem. Parametry mohou být "backup" pro zálohu, nebo "restore" pro obnovu.



