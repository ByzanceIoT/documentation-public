# Omezení konfigurace

## MQTT

### **normal\_mqtt\_hostname**

Hostname nebo IP adresa hlavního serveru.

| Typ | char\[128\] |
| --- | --- |
| Omezení | tisknutelné ASCII znaky zakončené terminační nulou |

### **normal\_mqtt\_port**

MQTT port hlavního serveru.

| Typ | 16 bit unsigned integer |
| --- | --- |
| Rozsah | 0 - 65535 |

### **backup\_mqtt\_hostname**

Hostname nebo IP adresa záložního serveru.

| Typ | char\[128\] |
| --- | --- |
| Omezení | tisknutelné ASCII znaky zakončené terminační nulou |

### **backup\_mqtt\_port**

MQTT port záložního serveru.

| Typ | 16 bit unsigned integer |
| --- | --- |
| Rozsah | 0 - 65535 |

### **mqtt\_username**

Přihlašovací jméno do MQTT brokeru.

| Typ | char\[48\] |
| --- | --- |
| Omezení | tisknutelné ASCII znaky zakončené terminační nulou |

### **mqtt\_password**

Přihlašovací heslo do MQTT brokeru.

| Typ | char\[48\] |
| --- | --- |
| Omezení | tisknutelné ASCII znaky zakončené terminační nulou |

## Ostatní

### **alias**

Alias zařízení, který si každý může nastavit pro lepší [identifikaci zařízení](identifikace-zarizeni.md).

| Typ | char\[64\] |
| --- | --- |
| Omezení | tisknutelné ASCII znaky zakončené terminační nulou |

### **mac**

Zjištění MAC adresy.

### **blreport**

Bootloader report. Zapnutí, nebo vypnutí výpisu hlavičky [bootloaderu](../architektura-fw/bootloader/) do konzole.

| Typ | boolean |
| --- | --- |
| Omezení | 0 nebo 1 |

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



