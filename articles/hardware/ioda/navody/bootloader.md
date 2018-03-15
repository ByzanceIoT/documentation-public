### Mód JUMP

Pokud není speciálně nastaven jiný mód, bootloader se sám přepne do módu JUMP. Ten sestává z několika kroků:

* Kontrola přitomnosti hlavní aplikace. Pokud hlavní aplikace není dostupná, dojde k přepnutí do command reřimu.
* Spuštění watchdogu \(pokud je nastaveno\) a případné nastavení na příslušnou hodnotu. Blíže vysvětleno v sekci [watchdog](link na watchdog).
* **Skok do hlavní aplikace**

### Mód FLASH

Do módu FLASH bootloader automaticky přechází, pokud je zapnutý ''flashflag'' \(více viz [aktualizace firmware](odkaz aktualizace firmware)\). V takovém případě potom následují tyto kroky:

* Načtení struktury s informacemi o novém firmware
* Validace a případná oprava velikosti, je-li to možné
* Vymazání interní paměti
* Překopírování všech částí binárky z externí paměti do mikrokontroléru
* Aktualizace informací o novém firmware v mikrokontroléru

Pokud všechny tyto kroky proběhnou v pořádku, následuje

* Vypnutí ''flashflag''
* Zapnutí ''launched'', který slouží ke kontrole funkčnosti nového firmware. Nový firmware tento flag opětovně vypne a tím potvrdí svou funkčnost. Pokud tak nenasatane [watchdog](ODKAZ WATCHDOG)  restartuje mikrokontrolér a spustí poslední funkční verzi firmware pomocí funkce [autobackup](Odkaz na autobackup) 
* Vypnutí oprávnění uděleného v proměnné ''trusted'', díky čemuž se firmware označí za potencionálně nefunkční. Firmware bude znovu označený za ověřený poté, co splní příslušná kritéria procesu [autobackup](odkaz autobackup). Poté  co je nový firmware označen flagem "trusted" záložní firmware je přepsan firmwarem aktuálním.

### Mód RESTORE

Tento mód je velmi podobný módu FLASH. Pokud bootloader detekuje zapnutý flag ''launched'' \(tzn. binárka se nedokázala spustit jako hlavní program\), mód je automaticky vyvolán a poslední funkční firmware je obnoven. Flagy ''flashflag'', ''launched'' a ''trusted'' zůstávají nezměněny.

### Mód COMMANDS

Do módu COMMANDS je možné vstoupit několika způsoby

* První spuštění bootloaderu na novém mikrokontroléru
* Kombinací tlačítek \(viz [command režim](odkaz na bootloader comand režim)\)
* Chybí hlavní aplikace
* Bootloader není nakonfigurován \(vypnutá proměnná ''configured'' v [command režimu TO DO](odkaz na command režim).

### Mód FACTORY RESET

Do módu FACTORY RESET se může dostat bootloader tak, že uživatel stiskne zároveň tlačítka ''restart'' a ''user'', pustí ''restart'' a tlačítko ''user'' drží dlouhou dobu, zpravidla více jak 10 sekund. Mikrokontrolér je nastaven do [defaultních hodnot](odkaz na defaultní hodnoty) a po této proceduře se přepne do režimu COMMANDS, stejně jako by byl mikrokontrolér poprvé spuštěn.

### Vývojový diagram



## Command režim

V command režimu je možné pomocí příkazů po sériové lince ověřovat a nastavovat konfigurační parametry Bootloaderu.

Do command režimu bootloaderu je možno vstopit následujícím způsobem

1. podržet RESET a USER tlačítko dohromady
2. pustit RESET tlačítko
3. počkat několik sekund, než zhasne červená LED
4. pustit USER tlačítko

Při prvním spuštění nebo při položce configured=0 bootloader skáče do command režimu automaticky.

### Příkazy bez parametru

* **ping** - ping, pro testovací účely
* **help** - vypíše nápovědu do konzole
* **overview** - vypíše aktuální hodnotu všech parametrů, které jsou v bootloaderu nastaveny
* **restart** - restartuje Iodu. \[\[tutorial:restart\|Dokumentace k restartu\]\].
* **target** -Typ desky. TODO 
* **fullid** - vypíše FULL ID procesoru. [odkaz na fullid](TODO) 
* **launch\_reset** - Pokud bylo předchozí spuštění firmware neúspěšné a není žádná validní binárka k obnovení, je třeba nahrát validní binárku a poté napsat příkaz ''launch\_reset''.
* **defaults** - Veškeré nastavení se obnoví do [defaultního nastavení](TO DO ODKAZ).

### Příkazy s parametrem i bez

Více informací k MQTT připojení je možno nalézt v sekci [Komunikace se servery](/articles/hardware/komunikace-se-servery.md).

* **normal\_mqtt\_hostname** - Hostname, na kterém běží hlavní Homer.
* **normal\_mqtt\_port** -  Hlavní port, na kterém běží Homer.
* **backup\_mqtt\_hostname** - Záložní hostname, na kterém běží Homer.
* **backup\_mqtt\_port** - Záložní port, na kterém běží Homer. 
* **mqtt\_username** - Záložní jméno pro přihlášení k Homerovi.
* **backup\_mqtt\_password** - Záložní heslo pro přihlášení k Homerovi.

* **alias** - Alias zařízení, který si každý může nastavit pro lepší [identifikaci zařízení](/articles/hardware/ioda/navody/identifikace-zarizeni.md).

* **mac** - Zjištění MAC adresy.

* **blreport** - Bootloader report. Zapnutí, nebo vypnutí výpisu hlavičky [bootloader](//articles/hardware/ioda/navody/bootloader.md)u do konzole.

* **wdenable** - Zapnutí [watchdogu](/byzance_documentation/hardware_intro/features/watchdog.md).

* **wdtime** - Nastavení periody resetu [watchdogu](/byzance_documentation/hardware_intro/features/watchdog.md).

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

### Příkazy pouze s parametrem

* **info** - Informace k dané komponentě.
  Parametry mohou být "bootloader", "firmware", "buffer", "backup".
* **memsize** - Velikost oddílu, který je vyhrazen pro danou komponentu.
  Parametry mohou být "bootloader", "firmware", "buffer", "backup".
* **intmem** - Zformátuje paměť.
  Parametry mohou být "intmem" nebo "extmem". \[\[memory:internal\|Informace o interní paměti\]\].
* **firmware** - Práce si firmwarem.
  Parametry mohou být "backup" pro zálohu, nebo "restore" pro obnovu.

---

### Default Configuration Values

"_If you are in the configuration mode, the LED lights up blue"_

Pokud se poprvé nahraje binárka bootloaderu do mikrokontroléru, bootloader sám umí detekovat, že target není zatím nakonfigurován. Nastala-li porucha některé hodnoty, bootloader danou hodnotu umí opravit. K nastavení výchozích vlastností slouží soubor`struct_defaults.h`s podobným obsahem tomuto

### Important notice !!!



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





