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
DEFAULTS_CONF_WEBVIEW             1                   // user configurable via Bootloader & Portal ( 0 or 1)
DEFAULTS_CONF_WEBPORT             80                  // user configurable via Bootloader & Portal ( 80 - 9999)
DEFAULTS_CONF_TIMEOFFSET          0                   // user configurable
DEFAULTS_CONF_TIMESYNC            1                   // user configurable
DEFAULTS_CONF_LOWPANBR            0                   // user configurable
DEFAULTS_CONF_RESTARTBL           0                   // user configurable
DEFAULTS_CONF_AUTOJUMP            300                 // user configurable via Bootloader & Portal

// binary defaults
DEFAULTS_BIN_VERSION_NAME            'v'            // ** managed by byzance (according http://semver.org) 
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

**DEFAULTS\_CONF\_AUTOBACKUP**: The Backup feature was designed to protect you against your own **mistakes** in Firmware while\(true\) {} for example. You have 2 options to have an active backup. The first is** Auto Backup **and second is **Static Backup. Value 1 for Auto backup, 0 for Static Backup \(If you are doing this manualy - we recomend set Backup Firmware immidiately\).**

Remember that you can do this automatically with \(Releas Manager\) on our portal. Or with Rest Api with our Core Server.

> **Auto Backup: ** Which is a mode that always keeps the firmware running for at least 30 seconds and successfully sommunicated with main Server in Cloud. Firmware will automaticaly make a copy of you actual running firmware to  backup part of memmory. So when you upload a new firmware that contains errors, Bootloader will automaticaly start the previous one from Backup. The version you uploaded is also marked i Portal by the server as unstable.
>
> **Static Backup: **You specify what static version of the backup you want on your device. We recommend using it in critical areas of industry. For example, when driving traffic lights. \(When the primary program fails - the backup is at least flashing orange\). The downside is that if the backup fails and bugs in backup does not allow the device to connect to server, you're fucked. You have to to fix the device yourself.

**DEFAULTS\_CONF\_WEBVIEW**: For easier programming and overview, we've created a simple web page that shows current events and information on hardware. You have to enable this register to show it.  \(make it available on the local network\). Warning! \(Its not available from outside from public internet\) The IP address is assigned by your DHCP server. Remember that you can do this automatically with on our portal. Or with Rest Api with our Core Server.

**DEFAULTS\_CONF\_WEBPORT**: The web port is the port on which the device listens on local network. \(Its not available from outside from public internet\)  This default port is used only for default development portal with basic informations. You can make your own website but dont use, the same webpost. Our recommendation is also to avoid all known ports. For example, databases etc. Do not forget for webpage access, that it must be allowed by **DEFAULTS\_CONF\_WEBVIEW** constant. Remember that you can do this automatically with on our portal. Or with Rest Api with our Core Server.

**DEFAULTS\_CONF\_CONFIGURED**: After all values are configured,  you have to set Flag Register DEFAULTS\_CONF\_CONFIGURED to value "1" \(number\). This indicates that the device is fully configured. After restart of on every start, the device \(bootloader\) will automatically search for the main Firmware first or Backup. When Bootloader does not find the Main Firmware or Backup, Bootloader is automaticaly activated.

**DEFAULTS\_CONF\_AUTOJUMP:** in some case, the device enters into configuration mode \(bootloader\). Therefore, there is this constant that automatically restarts and and switches the device back to the firmware. If this constant is not set, you risk that the device will be permanently active in the configuration mode and will not be able to update it remotely.

---

# Princip detekce a nastavení nevalidních hodnot v bootloaderu

Proces detekce nevalidních hodnot se spouští ihned po startu bootloaderu při každém spuštění. Existují 2 typy detekce nevalidních hodnot

* nevalidní \(celá\) struktura
* nevalidní položka struktury

Pokud je detekována celá nevalidní struktura \(je složena z hodnot 0xFF → smazaná flash paměť\), tak se celá struktura nahradí defaultními daty \(viz tabulka výše\) a uloží do flash paměti. Tato možnost nastává zpravidla při prvním spuštění bootloaderu na novém mikrokontroléru. Výhodou tohoto režimu je, že je poměrně rychlý.

Druhá možnost je oprava nevalidní položky struktury. V tomto případě se načítají, porovnávají, opravují a ukládají jednotlivé položky struktur, což zabere řádově více času a brzdí to bootloader před skokem do programu. Tato varianta může nastat buď při havárii programu \(nemělo by se to stávat kvůli zápisu přes žurnál\), nebo častěji při aktualizaci bootloaderu, kdy v nové verzi bootloaderu přibyde v některé struktuře nová položka, se kterou se dříve nepočítalo. Tímto způsobem se automaticky nastaví na rozumnou defaultní hodnotu.

