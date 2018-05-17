# Omezení konfigurace

## MQTT

Připojení zařízení k serverům Byzance využívá technologii MQTT. 

{% page-ref page="../konektivita/komunikace-s-portalem.md" %}

Z hlediska bezpečnosti se používá hlavní a záložní MQTT server. 

{% page-ref page="../konektivita/prepinani-mezi-servery.md" %}

### **normal\_mqtt\_hostname**

Hostname nebo IP adresa hlavního serveru.

| typ | char\[128\] |
| --- | --- | --- | --- | --- |
| omezení | tisknutelné ASCII znaky zakončené terminační nulou |
| výchozí hodnota | 192.168.65.179 |
| možnost číst | ano, uživatel |
| možnost nastavit | ano, uživatel |

### **normal\_mqtt\_port**

MQTT port hlavního serveru.

| typ | 16 bit unsigned integer |
| --- | --- | --- | --- | --- |
| omezení | 0 - 65535 |
| výchozí hodnota | 1881 |
| možnost číst | ano, uživatel |
| možnost nastavit | ano, uživatel |

### **backup\_mqtt\_hostname**

Hostname nebo IP adresa záložního serveru.

| typ | char\[128\] |
| --- | --- | --- | --- | --- |
| omezení | tisknutelné ASCII znaky zakončené terminační nulou |
| výchozí hodnota | 192.168.65.179 |
| možnost číst | ano, uživatel |
| možnost nastavit | ano, uživatel |

### **backup\_mqtt\_port**

MQTT port záložního serveru.

| typ | 16 bit unsigned integer |
| --- | --- | --- | --- | --- |
| omezení | 0 - 65535 |
| výchozí hodnota | 1881 |
| možnost číst | ano, uživatel |
| možnost nastavit | ano, uživatel |

### **mqtt\_username**

Přihlašovací jméno do MQTT brokeru.

| typ | char\[48\] |
| --- | --- | --- | --- | --- |
| omezení | tisknutelné ASCII znaky zakončené terminační nulou |
| výchozí hodnota | user |
| možnost číst | uživatelsky ne, pouze interně |
| možnost zapisovat | ano, uživatel |

### **mqtt\_password**

Přihlašovací heslo do MQTT brokeru.

| typ | char\[48\] |
| --- | --- | --- | --- | --- |
| omezení | tisknutelné ASCII znaky zakončené terminační nulou |
| výchozí hodnota | pass |
| možnost číst | uživatelsky ne, pouze interně |
| možnost zapisovat | ano, uživatel |

## Ostatní

### **alias**

Alias zařízení, který si každý může nastavit pro lepší [identifikaci zařízení](identifikace-zarizeni.md).

| typ | char\[64\] |
| --- | --- | --- | --- | --- |
| omezení | tisknutelné ASCII znaky zakončené terminační nulou |
| výchozí hodnota | BYZANCE |
| možnost číst | ano, uživatel |
| možnost zapisovat | ano, uživatel |

### **mac**

Zjištění MAC adresy.

| typ | char\[32\] |
| --- | --- | --- | --- | --- |
| omezení | 48 bitů; šestice dvojciferných hexadecimálních čísel oddělených dvojtečkou |
| výchozí hodnota | ff:ff:ff:ff:ff:ff |
| možnost číst | ano, uživatel |
| možnost zapisovat | pouze při první konfiguraci, většinou ve výrobě |

### **blreport**

Bootloader report. Zapnutí, nebo vypnutí výpisu hlavičky [bootloaderu](../architektura-fw/bootloader/) do konzole.

| typ | boolean |
| --- | --- | --- | --- | --- |
| omezení | 0, 1 |
| výchozí hodnota | 0 |
| možnost číst | ano, uživatel |
| možnost zapisovat | ano, uživatel |

### **wdenable**

Zapnutí [watchdogu](../funkcionality/watchdog.md).

| typ | boolean |
| --- | --- | --- | --- | --- |
| omezení | 0, 1 |
| výchozí hodnota | 1 |
| možnost číst | ano, uživatel |
| možnost zapisovat | ano, uživatel |

### **wdtime**

Nastavení periody resetu [watchdogu](../funkcionality/watchdog.md).

| typ | integer |
| --- | --- | --- | --- | --- |
| omezení | 0 - 32 |
| výchozí hodnota | 30 |
| možnost číst | ano, uživatel |
| možnost zapisovat | ano, uživatel |

### **autobackup**

Funkce, která zajišťuje, zajišťuje zálohu starého firmware při doručení nového.

| typ | boolean |
| --- | --- | --- | --- | --- |
| omezení | 0, 1 |
| výchozí hodnota | 0 |
| možnost číst | ano, uživatel |
| možnost zapisovat | ano, uživatel |

### **netsource**

Zdroj, odkud bere zařízení internet.

| typ | enum |
| --- | --- | --- | --- | --- |
| omezení | disabled, ethernet, wifi, 6lowpan, gsm |
| výchozí hodnota | ethernet |
| možnost číst | ano, uživatel |
| možnost zapisovat | ano, uživatel |

### **configured**

při prvním spuštění bootloader naběhne vždy do Command režimu a čeká na konfiguraci všech parametrů. Až jsou parametry nastaveny, ''configured'' se přepne na 1 a tím se dá zařízení najevo, že je již plně nakonfigurováno a příště bude už nabíhat do normálního programu.

| typ | boolean |
| --- | --- | --- | --- | --- |
| omezení | 0, 1 |
| výchozí hodnota | 1 |
| možnost číst | ano, uživatel |
| možnost zapisovat | ano, uživatel |

### **webview**

Zapnutí nebo vypnutí funkcionality [webového rozhraní](../funkcionality/webove-rozhrani/).

| typ | boolean |
| --- | --- | --- | --- | --- |
| omezení | 0, 1 |
| výchozí hodnota | 1 |
| možnost číst | ano, uživatel |
| možnost zapisovat | ano, uživatel |

### **webport**

Port, na kterém bude přístupno [webové rozhraní](../funkcionality/webove-rozhrani/).

| typ | 16 bit unsigned integer |
| --- | --- | --- | --- | --- |
| omezení | 0 - 65535 |
| výchozí hodnota | 80 |
| možnost číst | ano, uživatel |
| možnost zapisovat | ano, uživatel |

### **timeoffset**

Slouží pro lokalizovanou [práci s časem](../tutorialy/prace-s-datem-a-casem-rtc.md). Nastavení offsetu lokálního času RTC od UTC.

| typ | 32 bit unsigned integer |
| --- | --- | --- | --- | --- |
| omezení |  4294967296; vyjadřuje sekundy |
| výchozí hodnota | 0 |
| možnost číst | ano, uživatel |
| možnost zapisovat | ano, uživatel |

### **timesync**

Slouží pro zapnutí [synchronizace času](../tutorialy/prace-s-datem-a-casem-rtc.md) mezi servery Byzance a RTC.

| typ | boolean |
| --- | --- | --- | --- | --- |
| omezení |  0, 1 |
| výchozí hodnota | 1 |
| možnost číst | ano, uživatel |
| možnost zapisovat | ano, uživatel |

### **lowpanbr**

Zapnutí funkce [lowpan border router](../konektivita/6lowpan.md).

| typ | boolean |
| --- | --- | --- | --- | --- |
| omezení |  0, 1 |
| výchozí hodnota | 0 |
| možnost číst | ano, uživatel |
| možnost zapisovat | ano, uživatel |

### **restartbl**

Identifikátor pro [restart zařízení do bootloaderu](../architektura-fw/bootloader/).

| typ | boolean |
| --- | --- | --- | --- | --- |
| omezení | 0, 1 |
| výchozí hodnota | 0 |
| možnost číst | ano, uživatel |
| možnost zapisovat | ano, uživatel |

### **revision**

Zjištění [revize zařízení](../funkcionality/revize.md)

| typ | 32 bit unsigned integer |
| --- | --- | --- | --- | --- |
| omezení | 4 byte hexadecimální číslo 0x00000000-0xFFFFFFFF |
| výchozí hodnota | 0xFFFFFFFF |
| možnost číst | ano, uživatel |
| možnost zapisovat | pouze při první konfiguraci, většinou ve výrobě |

### **autojump**

Nastavení funkce [autojump](omezeni-konfigurace.md#autojump).

| typ | 32 bit unsigned integer |
| --- | --- | --- | --- | --- |
| omezení | 0 - 4294967296 |
| výchozí hodnota | 300 |
| možnost číst | ano, uživatel |
| možnost zapisovat | ano, uživatel |

