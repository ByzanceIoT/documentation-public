# Konfigurace

### **alias**

Alias zařízení, který si každý může nastavit pro lepší [identifikaci zařízení](../identifikace-zarizeni.md). Změna se projeví okamžitě.

| typ | char\[64\] |
| :--- | :--- |
| omezení | tisknutelné ASCII znaky zakončené terminační nulou |
| výchozí hodnota | BYZANCE |
| možnost číst | ano, uživatel |
| možnost zapisovat | ano, uživatel |
| confighash | ano |

### **mac**

Zjištění MAC adresy.

| typ | char\[32\] |
| :--- | :--- |
| omezení | 48 bitů; šestice dvojciferných hexadecimálních čísel oddělených dvojtečkou |
| výchozí hodnota | ff:ff:ff:ff:ff:ff |
| možnost číst | ano, uživatel |
| možnost zapisovat | pouze při první konfiguraci, většinou ve výrobě |
| confighash | ne |

### **blreport**

Bootloader report. Zapnutí, nebo vypnutí výpisu hlavičky [bootloaderu](../bootloader/) do konzole. Změna se projeví po restartu zařízení.

| typ | boolean |
| :--- | :--- |
| omezení | 0, 1 |
| výchozí hodnota | 0 |
| možnost číst | ano, uživatel |
| možnost zapisovat | ano, uživatel |
| confighash | ano |

### **wdenable**

Zapnutí [watchdogu](../../knowledge-base/watchdog.md). Změna se projeví po restartu zařízení.

| typ | boolean |
| :--- | :--- |
| omezení | 0, 1 |
| výchozí hodnota | 1 |
| možnost číst | ano, uživatel |
| možnost zapisovat | ano, uživatel |
| confighash | ano |

### **wdtime**

Nastavení periody resetu [watchdogu](../../knowledge-base/watchdog.md). Změna se projeví po restartu zařízení.

| typ | integer |
| :--- | :--- |
| omezení | 0 - 32 |
| výchozí hodnota | 30 |
| možnost číst | ano, uživatel |
| možnost zapisovat | ano, uživatel |
| confighash | ano |

### **autobackup**

Funkce, která zajišťuje, zajišťuje zálohu starého firmware při doručení nového. Změna se projeví při dalším updatu zařízení.

| typ | boolean |
| :--- | :--- |
| omezení | 0, 1 |
| výchozí hodnota | 0 |
| možnost číst | ano, uživatel |
| možnost zapisovat | ano, uživatel |
| confighash | ano |

### **netsource**

Zdroj, odkud bere zařízení internet. Změna se projeví po restartu zařízení.

| typ | enum |
| :--- | :--- |
| omezení | disabled, ethernet, wifi, 6lowpan, gsm |
| výchozí hodnota | ethernet |
| možnost číst | ano, uživatel |
| možnost zapisovat | ano, uživatel |
| confighash | ano |

### **configured**

při prvním spuštění bootloader naběhne vždy do Command režimu a čeká na konfiguraci všech parametrů. Až jsou parametry nastaveny, ''configured'' se přepne na 1 a tím se dá zařízení najevo, že je již plně nakonfigurováno a příště bude už nabíhat do normálního programu. Změna se projeví po restartu zařízení.

| typ | boolean |
| :--- | :--- |
| omezení | 0, 1 |
| výchozí hodnota | 1 |
| možnost číst | ano, uživatel |
| možnost zapisovat | ano, uživatel |
| confighash | ano |

### **reconnect**

Nastavení času pro opětovné připojení k serverům, v případě chyby. Změna se projeví po restartu zařízení.

| typ | 32 bit unsigned integer |
| :--- | :--- |
| omezení | 0 -  4294967295 |
| výchozí hodnota | 15 |
| možnost číst | ano, uživatel |
| možnost zapisovat | ano, uživatel |
| confighash | ano |

### encryption

Zapnutí nebo vypnutí možnosti šifrování. Změna se projeví po restartu zařízení.

| typ | boolean |
| :--- | :--- |
| omezení | 0, 1 |
| výchozí hodnota | 0 |
| možnost číst | ano, uživatel |
| možnost zapisovat | ano, uživatel |
| confighash | ano |

### **webview**

Zapnutí nebo vypnutí funkcionality [webového rozhraní](../webove-rozhrani/). Změna se projeví po restartu zařízení.

| typ | boolean |
| :--- | :--- |
| omezení | 0, 1 |
| výchozí hodnota | 1 |
| možnost číst | ano, uživatel |
| možnost zapisovat | ano, uživatel |
| confighash | ano |

### **webport**

Port, na kterém bude přístupno [webové rozhraní](../webove-rozhrani/). Změna se projeví po restartu zařízení.

| typ | 16 bit unsigned integer |
| :--- | :--- |
| omezení | 0 - 65535 |
| výchozí hodnota | 80 |
| možnost číst | ano, uživatel |
| možnost zapisovat | ano, uživatel |
| confighash | ano |

### **timeoffset**

Slouží pro lokalizovanou [práci s časem](../../tutorialy/datum-a-cas-rtc.md). Nastavení offsetu lokálního času RTC od UTC. 

| typ | 32 bit unsigned integer |
| :--- | :--- |
| omezení | 4294967296; vyjadřuje sekundy |
| výchozí hodnota | 0 |
| možnost číst | ano, uživatel |
| možnost zapisovat | ano, uživatel |
| confighash | ano |

### **timesync**

Slouží pro zapnutí [synchronizace času](../../tutorialy/datum-a-cas-rtc.md) mezi servery Byzance a RTC.

| typ | boolean |
| :--- | :--- |
| omezení | 0, 1 |
| výchozí hodnota | 1 |
| možnost číst | ano, uživatel |
| možnost zapisovat | ano, uživatel |
| confighash | ano |

### **lowpanbr**

Zapnutí funkce [lowpan border router](../../konektivita/6lowpan.md). Změna se projeví po restartu zařízení.

| typ | boolean |
| :--- | :--- |
| omezení | 0, 1 |
| výchozí hodnota | 0 |
| možnost číst | ano, uživatel |
| možnost zapisovat | ano, uživatel |
| confighash | ano |

### **restartbl**

Identifikátor pro [restart zařízení do bootloaderu](../bootloader/) - po restartu zařízení zůstane v command režimu. Po přepnutí proměnné je třeba zařízení restartovat. Po vystoupení z bootloaderu se proměmná automaticky opět vynuluje.

| typ | boolean |
| :--- | :--- |
| omezení | 0, 1 |
| výchozí hodnota | 0 |
| možnost číst | ano, uživatel |
| možnost zapisovat | ano, uživatel |
| confighash | ne |

### **revision**

Zjištění revize zařízení

| typ | 32 bit unsigned integer |
| :--- | :--- |
| omezení | 4 byte hexadecimální číslo 0x00000000-0xFFFFFFFF |
| výchozí hodnota | 0xFFFFFFFF |
| možnost číst | ano, uživatel |
| možnost zapisovat | pouze při první konfiguraci, většinou ve výrobě |
| confighash | ne |

### **autojump**

Nastavení funkce autojump. Změna se projeví po restartu zařízení.

| typ | 32 bit unsigned integer |
| :--- | :--- |
| omezení | 300 - 4294967296 |
| výchozí hodnota | 300 |
| možnost číst | ano, uživatel |
| možnost zapisovat | ano, uživatel |
| confighash | ano |

### **lastpart**

Poslední validní část binárky v bufferu. Informace se ukládá každých 32 partů.

| typ | 32 bit unsigned integer |
| :--- | :--- |
| omezení | 0 - 4294967296 |
| výchozí hodnota | 0 |
| možnost číst | ano, uživatel |
| možnost zapisovat | automaticky |
| confighash | ne |

