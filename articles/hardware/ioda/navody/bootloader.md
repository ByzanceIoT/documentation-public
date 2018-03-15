




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





