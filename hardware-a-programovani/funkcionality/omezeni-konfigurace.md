# Omezení konfigurace

## MQTT

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

### **blreport**

Bootloader report. Zapnutí, nebo vypnutí výpisu hlavičky [bootloaderu](../architektura-fw/bootloader/) do konzole.

| typ | boolean |
| --- | --- | --- | --- | --- |
| omezení | 0, 1 |
| výchozí hodnota | 0 |
| možnost číst | ano, uživatel |
| možnost zapisovat | ano, uživatel |

### **wdenable**

Zapnutí [watchdogu](watchdog.md).

### **wdtime**

Nastavení periody resetu [watchdogu](watchdog.md).

### **autobackup**

Funkce, která zajišťuje, zajišťuje zálohu starého firmware při doručení nového.

### **netsource**

Zdroj, odkud bere zařízení internet.

### **configured**

při prvním spuštění bootloader naběhne vždy do Command režimu a čeká na konfiguraci všech parametrů. Až jsou parametry nastaveny, ''configured'' se přepne na 1 a tím se dá zařízení najevo, že je již plně nakonfigurováno a příště bude už nabíhat do normálního programu.

### **webview**

Zapnutí nebo vypnutí funkcionality [webového rozhraní](webove-rozhrani/).

### **webport**

Port, na kterém bude přístupno [webové rozhraní](webove-rozhrani/).

### **timeoffset**

Slouží pro lokalizovanou [práci s časem](../tutorialy/prace-s-datem-a-casem-rtc.md). Nastavení offsetu lokálního času RTC od UTC.

### **timesync**

Slouží pro zapnutí [synchronizace času](../tutorialy/prace-s-datem-a-casem-rtc.md) mezi servery Byzance a RTC.

### **lowpanbr**

Zapnutí funkce [lowpan border router](../konektivita/6lowpan.md).

### **restartbl**

Identifikátor pro [restart zařízení do bootloaderu](../architektura-fw/bootloader/).

### **revision**

Zjištění [revize zařízení](revize.md)



