# Omezení konfigurace

## MQTT

### **normal\_mqtt\_hostname**

Hostname, na kterém běží hlavní Homer.

### **normal\_mqtt\_port**

Hlavní port, na kterém běží Homer.

### **backup\_mqtt\_hostname**

Záložní hostname, na kterém běží Homer.

### **backup\_mqtt\_port**

Záložní port, na kterém běží Homer. 

### **mqtt\_username**

Jméno pro přihlášení k Homerovi.

### **mqtt\_password**

Heslo pro přihlášení k Homerovi.

## Ostatní

* **alias** - Alias zařízení, který si každý může nastavit pro lepší [identifikaci zařízení](identifikace-zarizeni.md).
* **mac** - Zjištění MAC adresy.
* **blreport** - Bootloader report. Zapnutí, nebo vypnutí výpisu hlavičky [bootloaderu](../architektura-fw/bootloader/) do konzole.
* **wdenable** - Zapnutí [watchdogu](watchdog.md).
* **wdtime** - Nastavení periody resetu [watchdogu](watchdog.md).
* **autobackup** - Funkce, která zajišťuje, zajišťuje zálohu starého firmware při doručení nového.
* **netsource** - Zdroj, odkud bere zařízení internet.
* **configured** - při prvním spuštění bootloader naběhne vždy do Command režimu a čeká na konfiguraci všech parametrů. Až jsou parametry nastaveny, ''configured'' se přepne na 1 a tím se dá zařízení najevo, že je již plně nakonfigurováno a příště bude už nabíhat do normálního programu.
* **webview** - Zapnutí nebo vypnutí funkcionality [webového rozhraní](webove-rozhrani/).
* **webport** - Port, na kterém bude přístupno [webové rozhraní](webove-rozhrani/).
* **timeoffset** - Slouží pro lokalizovanou [práci s časem](../tutorialy/prace-s-datem-a-casem-rtc.md). Nastavení offsetu lokálního času RTC od UTC.
* **timesync** - Slouží pro zapnutí [synchronizace času](../tutorialy/prace-s-datem-a-casem-rtc.md) mezi servery Byzance a RTC.
* **lowpanbr** - Zapnutí funkce [lowpan border router](../konektivita/6lowpan.md).
* **restartbl** - Identifikátor pro [restart zařízení do bootloaderu](../architektura-fw/bootloader/).
* **revision** - Zjištění [revize zařízení](revize.md)



