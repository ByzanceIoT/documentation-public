# Defaultní hodnoty

Pokud se poprvé nahraje binárka bootloaderu do mikrokontroléru, bootloader sám umí detekovat, že target není zatím nakonfigurován. Nastala-li porucha některé hodnoty, bootloader danou hodnotu umí opravit. K nastavení výchozích vlastností slouží soubor`struct_defaults.h`s podobným obsahem tomuto

```cpp
// defaultní hodnoty pro MQTT hlavní a záložní broker
DEFAULTS_MQTT_HOSTNAME                "192.168.65.179"
DEFAULTS_MQTT_PORT                    1881
DEFAULTS_MQTT_USERNAME                "user"
DEFAULTS_MQTT_PASSWORD                "pass"

// velikost devlistu
DEFAULTS_DEVLIST_COUNTER            0

// konfigurační struktura
DEFAULTS_CONF_FLASHFLAG            0
DEFAULTS_CONF_AUTOBACKUP            0
DEFAULTS_CONF_BOOTLOADER_REPORT        0
DEFAULTS_CONF_WATCHDOG_ENABLED                1
DEFAULTS_CONF_WATCHDOG_TIME            30
DEFAULTS_CONF_NETSOURCE                NETSOURCE_ETHERNET
DEFAULTS_CONF_CONFIGURED            0
DEFAULTS_CONF_LAUNCHED                0
DEFAULTS_CONF_ALIAS                "DEFAULT"
DEFAULTS_CONF_TRUSTED                TRUSTED_NONE
DEFAULTS_CONF_BACKUPTIME            60
DEFAULTS_CONF_WEBVIEW                1
DEFAULTS_CONF_WEBPORT                80
DEFAULTS_CONF_TIMEOFFSET            0
DEFAULTS_CONF_TIMESYNC                1
DEFAULTS_CONF_LOWPANBR                0
DEFAULTS_CONF_RESTARTBL            0
DEFAULTS_CONF_AUTOJUMP				300

// informace o wifi čipu (zastaralé, nyní nepoužito)
DEFAULTS_WIFI_VERSION_NAME            'V'
DEFAULTS_WIFI_VERSION_MAJOR            0
DEFAULTS_WIFI_VERSION_MINOR            0
DEFAULTS_WIFI_VERSION_PATCH            0
DEFAULTS_WIFI_MAC                "00:00:00:00:00:00"
DEFAULTS_WIFI_ESPID                0
DEFAULTS_WIFI_FLASHID                0
DEFAULTS_WIFI_FLASHSIZE            0
DEFAULTS_WIFI_FLASHSPEED            0

// přihlašovací údaje wifi (zastaralé, nyní nepoužito)
DEFAULTS_WIFI_CRED_SSID            (const char*)"SSID"
DEFAULTS_WIFI_CRED_PASSWORD            (const char*)"PASSWORD"

// struktura binárky (platí pro všechny typy binárek)
DEFAULTS_BIN_VERSION_NAME               'V'
DEFAULTS_BIN_VERSION_MAJOR            0
DEFAULTS_BIN_VERSION_MINOR            0
DEFAULTS_BIN_VERSION_PATCH            0
DEFAULTS_BIN_SIZE                0
DEFAULTS_BIN_CRC                0
DEFAULTS_BIN_TIMESTAMP                0
DEFAULTS_BIN_BUILD_ID                "DEFAULT"
DEFAULTS_BIN_NAME                "DEFAULT"
DEFAULTS_BIN_VALID                0
DEFAULTS_BIN_STATE                BINSTRUCT_STATE_INVALID
```

# Princip detekce a nastavení nevalidních hodnot v bootloaderu

Proces detekce nevalidních hodnot se spouští ihned po startu bootloaderu při každém spuštění. Existují 2 typy detekce nevalidních hodnot

* nevalidní \(celá\) struktura
* nevalidní položka struktury

Pokud je detekována celá nevalidní struktura \(je složena z hodnot 0xFF → smazaná flash paměť\), tak se celá struktura nahradí defaultními daty \(viz tabulka výše\) a uloží do flash paměti. Tato možnost nastává zpravidla při prvním spuštění bootloaderu na novém mikrokontroléru. Výhodou tohoto režimu je, že je poměrně rychlý.

Druhá možnost je oprava nevalidní položky struktury. V tomto případě se načítají, porovnávají, opravují a ukládají jednotlivé položky struktur, což zabere řádově více času a brzdí to bootloader před skokem do programu. Tato varianta může nastat buď při havárii programu \(nemělo by se to stávat kvůli zápisu přes žurnál\), nebo častěji při aktualizaci bootloaderu, kdy v nové verzi bootloaderu přibyde v některé struktuře nová položka, se kterou se dříve nepočítalo. Tímto způsobem se automaticky nastaví na rozumnou defaultní hodnotu.

