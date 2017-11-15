# Bootloader a Command režim

Bootloader je firmware nahraný v zařízení Byzance, které udržuje **základní konfiguraci zařízení** a obsluhuje spuštění hlavního uživatelského programu. Bootloder umožňuje nastavení jeho parametrů v command režimu, zasíláním příkazů po sériové lince.

**Overview**

1. [Spuštění Bootloaderu](zakladni-prehled)
  1. [Činnost bootloaderu](#činnost-bootloaderu)
   2. [Mód JUMP](#mód-jump)
   3. [Mód FLASH](#mód-flash)
2. [Command režim](#command-režim)
3. [Default Configuration Values](#default-configuration-values)

## Základní Přehled

FIXME jak ho vyvolat?!

Vstup do bootloaderu je vizuálně signalizován [Led modulem TO DO odkaz na ledmodul](odkaz na ledmodul).

Každé zařízení má v sobě nahraných více do jisté míry nezávislých programů. Typicky jde o tyto:

* bootloader,
* hlavní program,
* záložní program,
* programový buffer.

Každý program má ve FLASH paměti vyhrazeno pevné místo, tj. má [danou počáteční adresu a max. velikost - TO DO odkaz](ODKAZ na adresaci).

### Činnost bootloaderu

Po zapnutí napájení zařízení vždy začne vykonávat instrukce z bootloaderu. Úkolem bootloaderu je zajistit aktualizaci hlavního programu zařízení, obnovení v případě nefunkčního hlavního firmware a nastavení některých konfiguračních dat.

### Mód JUMP

Pokud není nastaven jiný mód, bootloader se sám přepne do módu JUMP. Ten sestává z několika kroků:

* Kontrola, jestli je přítomna hlavní aplikace - pokud není, dojde k přepnutí do command\_mode.
* Zapnutí watchdogu \(pokud má být zapnut\) a případné nastavení na příslušnou hodnotu. Více v sekci [watchdog](link na watchdog).
* **Skok do hlavní aplikace**

### Mód FLASH

Do módu FLASH bootloader automaticky přechází, pokud je zapnutý ''flashflag'' \(více viz [aktualizace firmware TO DO](odkaz aktualizace firmware)\). V takovém případě potom následují tyto kroky:

* načtení struktury s informacemi o novém firmware,
* validace a případná oprava velikosti, je-li to možné a smyslné,
* vymazání interní paměti
* překopírování všech částí binárky z externí paměti do mikrokontroléru
* aktualizace informací v příslušné struktuře o novém firmware v mikrokontroléru

Pokud všechny tyto kroky proběhnou v pořádku, následuje

* vypnutí ''flashflag''
* zapnutí ''launched'', který by se měl v naběhnutém firmware vypnout a pokud tak nenastane \(binárka je vadná\), \[\[feature:watchdog\| watchdog\]\]  restartuje mikrokontrolér a spustí obnovu poslední funkční binárky vyrobené pomocí procesem \[\[feature:autobackup\|autobackup\]\] 
* vypnutí oprávnění udělené do proměnné ''trusted'', díky čemuž se firmware označí za potencionálně nefunkční. Oprávnění se zvýší až pokud běžící firmware splní příslušná kritéria procesu \[\[feature:autobackup\| autobackup\]\], kdy se automaticky může spustit záloha.

### Mód RESTORE

Tento mód je velmi podobný módu FLASH. Pokud bootloader detekuje zapnutý flag ''launched'' \(tzn. binárka se nedokázala spustit jako hlavní program\), mód je automaticky vyvolán a poslední funkční firmware je obnoven. Flagy ''flashflag'', ''launched'' a ''trusted'' zůstávají nezměněny.

### Mód COMMANDS

Do módu COMMANDS je možné vstoupit několika způsoby

* první spuštění bootloaderu na novém mikrokontroléru
* kombinací tlačítek \(viz [bootloader command režim TO DO ](odkaz na bootloader comand režim)\)
* chybějící hlavní aplikace
* bootloader není nakonfigurován \(vypnutá proměnná ''configured'' v [command režimu TO DO](odkaz na command režim).

### Mód WIFIAP

FIXME Nyní nepoužito

### Mód FACTORY RESET

Do módu FACTORY RESET se může dostat bootloader tak, že uživatel stiskne zároveň tlačítka ''restart'' a ''user'', pustí ''restart'' a tlačítko ''user'' drží dlouhou dobu, zpravidla více jak 10 sekund. Mikrokontrolér je nastaven do [defaultních hodnot TO DO](odkaz na defaultní hodnoty) a po této proceduře se přepne do režimu COMMANDS, stejně jako by byl mikrokontrolér poprvé spuštěn.

### Proces aktualizace hlavního programu v Device

FIXME aktuálně nevyužito a do budoucna device asi dostanou extmem a budou normálně pracovat s bufferem, je to bezpečnější a systematičtější

Terminologie:

* **aktuální** program je ten, který naposledy běžel z interní paměti Yody
* **nový** program je ten, který v Yodovi zatím neběžel

* Bootolader provede načtení parametrů **nového** programu z konfig. paměti a provedene validaci.

* Funkce autobackup je u device vždy zapnutá a nedá se vypnout.

* Homer dříve \[\[Yoda:upload\| nahrál do device\]\] do části nového programu **nový** program.

* Bootloader prohodí **aktuální** program s **novým** programem. Tím se z **nového** programu stane **aktuální**

* Zapíše se informace o **aktuálním** programu v Yodovi do konfigurační paměti.

* Na závěr bootloader skočí na začátek **aktuálního** programu a začne ho vykonávat.

### Aktualizace firmware

Aktualizace firmware je zdokumentována v sekci [Aktualizace firmware TO DO ](odkaz na aktualizaci firmware).  
Sestává ze 2 sad kroků

* **upload**, kdy se binárka přenese z Homera do Yody a uloží se do jeho externí paměti.
* **update**, kdy je yodovi specifikováno, co s danou binárkou má provést \(aktualizuje svůj firmware, nebo několik zařízení atd..\)

### Vývojový diagram

FIXME Zde bude obrázkový vývojový diagram co a jak

---

## Command režim

Do command režimu bootloaderu je možno vstopit následujícím způsobem

1. podržet RESET a USER tlačítko dohromady
2. pustit RESET tlačítko
3. počkat několik sekund, než zhasne červená LED
4. pustit USER tlačítko

Při prvním spuštění nebo při položce configured=0 bootloader skáče do command režimu automaticky.

### Příkazy bez parametru

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

### Příkazy s parametrem i bez

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

### Příkazy pouze s parametrem

* ''_info_'' - Informace k dané komponentě.
  Parametry mohou být "bootloader", "firmware", "buffer", "backup".
* ''_memsize_' - Velikost oddílu, který je vyhrazen pro danou komponentu.
  Parametry mohou být "bootloader", "firmware", "buffer", "backup".
* ''_intmem_'' - Zformátuje paměť.
  Parametry mohou být "intmem" nebo "extmem". \[\[memory:internal\|Informace o interní paměti\]\].
* ''_firmware_' - Práce si firmwarem.
  Parametry mohou být "backup" pro zálohu, nebo "restore" pro obnovu.

---

### Default Configuration Values

"_If you are in the configuration mode, the LED lights up blue"_

Pokud se poprvé nahraje binárka bootloaderu do mikrokontroléru, bootloader sám umí detekovat, že target není zatím nakonfigurován. Nastala-li porucha některé hodnoty, bootloader danou hodnotu umí opravit. K nastavení výchozích vlastností slouží soubor`struct_defaults.h`s podobným obsahem tomuto

### Important notice !!!

**Please keep in mind that what is stored in the database \(expected device setup\) is always superior to what is currently on the hardware. If you locally set a value and are not enabled \(Synchronize always with database = False\) in Portal. Core system \(server\) automatically synchronizes everything to the expected value by database.**

```cpp
// MQTT defaults
DEFAULTS_MQTT_HOSTNAME            (const char*)"192.168.65.179"  // user configurable via Bootloader & Portal
DEFAULTS_MQTT_PORT                (uint32_t)1881                 // user configurable via Bootloader & Portal
DEFAULTS_MQTT_USERNAME            (const char*)"user"            // user configurable via Bootloader & Portal
DEFAULTS_MQTT_PASSWORD            (const char*)"pass"            // user configurable via Bootloader & Portal


// configuration
DEFAULTS_CONF_FLASHFLAG           0                   // ** managed by byzance
DEFAULTS_CONF_AUTOBACKUP          0                   // user configurable ( 0 or 1) 
DEFAULTS_CONF_BOOTLOADER_REPORT   0                   // user configurable 
DEFAULTS_CONF_WATCHDOG_ENABLED    1                   // user configurable
DEFAULTS_CONF_WATCHDOG_TIME       30                  // user configurable 
DEFAULTS_CONF_NETSOURCE           NETSOURCE_ETHERNET  // user configurable ( 0 or 1)
DEFAULTS_CONF_CONFIGURED          0                   // user configurable ( 0 or 1)
DEFAULTS_CONF_LAUNCHED            0                   // ** managed by byzance
DEFAULTS_CONF_ALIAS               "DEFAULT"           // user configurable via Bootloader & Portal
DEFAULTS_CONF_TRUSTED             TRUSTED_NONE        // ** managed by byzance
DEFAULTS_CONF_BACKUPTIME          60                  // user configurable
DEFAULTS_CONF_WEBVIEW             1                   // user configurable via Bootloader & Portal ( 0 or 1)
DEFAULTS_CONF_WEBPORT             80                  // user configurable via Bootloader & Portal ( 80 - 9999)
DEFAULTS_CONF_TIMEOFFSET          0                   // user configurable
DEFAULTS_CONF_TIMESYNC            1                   // user configurable
DEFAULTS_CONF_LOWPANBR            0                   // user configurable
DEFAULTS_CONF_RESTARTBL           0                   // user configurable
DEFAULTS_CONF_AUTOJUMP            300                 // user configurable via Bootloader & Portal

// binary defaults
DEFAULTS_BIN_VERSION_NAME            'v'            // ** managed by byzance (according http://semver.org) - Automatic update
DEFAULTS_BIN_VERSION_MAJOR            0             // ** managed by byzance (number 0 - 99)   
DEFAULTS_BIN_VERSION_MINOR            0             // ** managed by byzance (number 0 - 99) 
DEFAULTS_BIN_VERSION_PATCH            0             // ** managed by byzance (number 0 - 99) 
DEFAULTS_BIN_SIZE                     0             // ** managed by byzance (number) - Automatic update
DEFAULTS_BIN_CRC                      0             // ** managed by byzance (number) - Automatic update
DEFAULTS_BIN_TIMESTAMP                0             // ** managed by byzance (number UX time stamp) - Automatic update 
DEFAULTS_BIN_BUILD_ID                "DEFAULT"                 // ** managed by byzance (UUID - 32 chars always) - Automatic update
DEFAULTS_BIN_NAME                    "DEFAULT"                 // ** managed by byzance (String 32 chars max) - Automatic update
DEFAULTS_BIN_STATE                    BINSTRUCT_STATE_INVALID  // ** managed by byzance (String 32 chars max) - Automatic update
```

### Technical Description

**DEFAULTS\_CONF\_AUTOBACKUP**: The Backup feature was designed to protect you against your own **mistakes** in Firmware while\(true\) {} for example. You have 2 options to have an active backup. The first is** Auto Backup **and second is **Static Backup. Value 1 for Auto backup, 0 for Static Backup \(If you are doing this manualy - we recomend set Backup Firmware immidiately\). **Remember that you can do this automatically with "Releas Manager" on our portal. Or with Rest Api with our Core Server.

* **Auto Backup: ** Which is a mode that always keeps the firmware running for at least 30 seconds and successfully sommunicated with main Server in Cloud. Firmware will automaticaly make a copy of you actual running firmware to  backup part of memmory. So when you upload a new firmware that contains errors, Bootloader will automaticaly start the previous one from Backup. The version you uploaded is also marked i Portal by the server as unstable.
* **Static Backup: **You specify what static version of the backup you want on your device. We recommend using it in critical areas of industry. For example, when driving traffic lights. \(When the primary program fails - the backup is at least flashing orange\). The downside is that if the backup fails and bugs in backup does not allow the device to connect to server, you're fucked. You have to to fix the device yourself.

**DEFAULTS\_CONF\_WEBVIEW**: For easier programming and overview, we've created a simple web page that shows current events and information on hardware. You have to enable this register to show it.  \(make it available on the local network\). Warning! \(Its not available from outside from public internet\) The IP address is assigned by your DHCP server. Remember that you can do this automatically with our portal. Or with Rest Api with our Core Server.

**DEFAULTS\_CONF\_WEBPORT**: The web port is the port on which the device listens on local network. \(Its not available from outside from public internet\)  This default port is used only for default development portal with basic informations. You can make your own website but dont use, the same webpost. Our recommendation is also to avoid all known ports. For example, databases etc. Do not forget for webpage access, that it must be allowed by **DEFAULTS\_CONF\_WEBVIEW** constant. Remember that you can do this automatically with our portal. Or with Rest Api with our Core Server.

**DEFAULTS\_CONF\_CONFIGURED**: After all values are configured,  you have to set Flag Register DEFAULTS\_CONF\_CONFIGURED to value "1" \(number\). This indicates that the device is fully configured. After restart of on every start, the device \(bootloader\) will automatically search for the main Firmware first or Backup. When Bootloader does not find the Main Firmware or Backup, Bootloader is automaticaly activated.

**DEFAULTS\_CONF\_AUTOJUMP:** in some case, the device enters into configuration mode \(bootloader\). Therefore, there is this constant that automatically restarts and and switches the device back to the firmware. If this constant is not set, you risk that the device will be permanently active in the configuration mode and will not be able to update it remotely. Remember that you can do this automatically with our portal. Or with Rest Api with our Core Server

**DEFAULTS\_CONF**_**ALIAS: **Alias is your own device name - Limited to 63 characters. For example "My Light" or "DEVICE\_X\_Y\_1". The Alias Name is accessible in firmware so you can used that for your private communication.  "MYCompany_\_LIGHT\_GENERATION1\_123423231". \_ Remember that you can do this automatically with our portal. Or with Rest Api with our Core Server. If you rename the device in the  our portal, or throw the API, It will automatically syncronizes with Hardware. Or the instructions are saved as soon as the device logs on.

---

### Princip detekce a nastavení nevalidních hodnot v bootloaderu

Proces detekce nevalidních hodnot se spouští ihned po startu bootloaderu při každém spuštění. Existují 2 typy detekce nevalidních hodnot

* nevalidní \(celá\) struktura
* nevalidní položka struktury

Pokud je detekována celá nevalidní struktura \(je složena z hodnot 0xFF → smazaná flash paměť\), tak se celá struktura nahradí defaultními daty \(viz tabulka výše\) a uloží do flash paměti. Tato možnost nastává zpravidla při prvním spuštění bootloaderu na novém mikrokontroléru. Výhodou tohoto režimu je, že je poměrně rychlý.

Druhá možnost je oprava nevalidní položky struktury. V tomto případě se načítají, porovnávají, opravují a ukládají jednotlivé položky struktur, což zabere řádově více času a brzdí to bootloader před skokem do programu. Tato varianta může nastat buď při havárii programu \(nemělo by se to stávat kvůli zápisu přes žurnál\), nebo častěji při aktualizaci bootloaderu, kdy v nové verzi bootloaderu přibyde v některé struktuře nová položka, se kterou se dříve nepočítalo. Tímto způsobem se automaticky nastaví na rozumnou defaultní hodnotu.

