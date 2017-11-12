# Default Configuration Values

"_If you are in the configuration mode, the LED lights up blue"_



Pokud se poprvé nahraje binárka bootloaderu do mikrokontroléru, bootloader sám umí detekovat, že target není zatím nakonfigurován. Nastala-li porucha některé hodnoty, bootloader danou hodnotu umí opravit. K nastavení výchozích vlastností slouží soubor`struct_defaults.h`s podobným obsahem tomuto

```cpp
// MQTT defaults
DEFAULTS_MQTT_HOSTNAME            (const char*)"192.168.65.179"  // user configurable
DEFAULTS_MQTT_PORT                (uint32_t)1881                   // user configurable
DEFAULTS_MQTT_USERNAME            (const char*)"user"            // user configurable
DEFAULTS_MQTT_PASSWORD            (const char*)"pass"            // user configurable

// configuration
DEFAULTS_CONF_FLASHFLAG           0                   // ** managed by byzance
DEFAULTS_CONF_AUTOBACKUP          0                   // user configurable ( 0 or 1) 
DEFAULTS_CONF_BOOTLOADER_REPORT   0                   // user configurable 
DEFAULTS_CONF_WATCHDOG_ENABLED    1                   // user configurable
DEFAULTS_CONF_WATCHDOG_TIME       30                  // user configurable 
DEFAULTS_CONF_NETSOURCE           NETSOURCE_ETHERNET  // user configurable ( 0 or 1)
DEFAULTS_CONF_CONFIGURED          0                   // user configurable ( 0 or 1)
DEFAULTS_CONF_LAUNCHED            0                   // ** managed by byzance
DEFAULTS_CONF_ALIAS               "DEFAULT"           // user configurable
DEFAULTS_CONF_TRUSTED             TRUSTED_NONE        // ** managed by byzance
DEFAULTS_CONF_BACKUPTIME          60                  // user configurable
DEFAULTS_CONF_WEBVIEW             1                   // user configurable via Bootloader & Portal
DEFAULTS_CONF_WEBPORT             80                  // user configurable via Bootloader & Portal
DEFAULTS_CONF_TIMEOFFSET          0                   // user configurable
DEFAULTS_CONF_TIMESYNC            1                   // user configurable
DEFAULTS_CONF_LOWPANBR            0                   // user configurable
DEFAULTS_CONF_RESTARTBL           0                   // user configurable
DEFAULTS_CONF_AUTOJUMP            300                 // user configurable via Bootloader & Portal

// binary defaults
DEFAULTS_BIN_VERSION_NAME            'v'            // ** managed by byzance
DEFAULTS_BIN_VERSION_MAJOR            0             // ** managed by byzance (number 0 - 99)   
DEFAULTS_BIN_VERSION_MINOR            0             // ** managed by byzance (number 0 - 99) 
DEFAULTS_BIN_VERSION_PATCH            0             // ** managed by byzance (number 0 - 99) 
DEFAULTS_BIN_SIZE                     0             // ** managed by byzance
DEFAULTS_BIN_CRC                      0             // ** managed by byzance
DEFAULTS_BIN_TIMESTAMP                0             // ** managed by byzance (number UX time stamp) 
DEFAULTS_BIN_BUILD_ID                "DEFAULT"                 // ** managed by byzance
DEFAULTS_BIN_NAME                    "DEFAULT"                 // ** managed by byzance
DEFAULTS_BIN_STATE                    BINSTRUCT_STATE_INVALID  // ** managed by byzance
```

## Technical Description

DEFAULTS\_CONF\_AUTOBACKUP: 

**DEFAULTS\_CONF\_CONFIGURED**: After all values are configured,  you have to set Flag Register DEFAULTS\_CONF\_CONFIGURED to value "1" \(number\). This indicates that the device is fully configured. After restart of on every start, the device \(bootloader\) will automatically search for the main Firmware first or Backup. When Bootloader does not find the Main Firmware or Backup, Bootloader is automaticaly activated.

**DEFAULTS\_CONF\_AUTOJUMP:** in some case, the device enters into configuration mode \(bootloader\). Therefore, there is this constant that automatically restarts and and switches the device back to the firmware. If this constant is not set, you risk that the device will be permanently active in the configuration mode and will not be able to update it remotely.

---

# Princip detekce a nastavení nevalidních hodnot v bootloaderu

Proces detekce nevalidních hodnot se spouští ihned po startu bootloaderu při každém spuštění. Existují 2 typy detekce nevalidních hodnot

* nevalidní \(celá\) struktura
* nevalidní položka struktury

Pokud je detekována celá nevalidní struktura \(je složena z hodnot 0xFF → smazaná flash paměť\), tak se celá struktura nahradí defaultními daty \(viz tabulka výše\) a uloží do flash paměti. Tato možnost nastává zpravidla při prvním spuštění bootloaderu na novém mikrokontroléru. Výhodou tohoto režimu je, že je poměrně rychlý.

Druhá možnost je oprava nevalidní položky struktury. V tomto případě se načítají, porovnávají, opravují a ukládají jednotlivé položky struktur, což zabere řádově více času a brzdí to bootloader před skokem do programu. Tato varianta může nastat buď při havárii programu \(nemělo by se to stávat kvůli zápisu přes žurnál\), nebo častěji při aktualizaci bootloaderu, kdy v nové verzi bootloaderu přibyde v některé struktuře nová položka, se kterou se dříve nepočítalo. Tímto způsobem se automaticky nastaví na rozumnou defaultní hodnotu.

