## Topic Info



Topic slouží k zjišťování informací a hodnot různcýh nastavení v Yodovi. Komunikuje se pomocí JSONů, které mají přesně dané parametry.

JSON z Homera do Yody má 1 povinný label, který vypadají takto:

**Request:**

```
 {
   "mid"            : "SOME ID"
 }
```

V labelu „mid“ je nějaké ID zprávy, které generuje Homer Yodovi. Yoda mu stejné`mid`vrací zpátky.

Pokud vše proběhne v pořádku, v odpovědi se vytvoří label „status“, který může nabývat hodnot „ok“ nebo „error“.

* Pokud label „status“ nabývá hodnoty „error“, vytvoří se nový label „error“, v němž je popis chyby, která nastala.
* Pokud label „status“ nabývá hodnoty „ok“, vytvoří se ostatní labely podle kontkrétní informace, která je zjišťována.

### Informace o "target"

Přistupuje se do něj takto`XXXXXXXXXXXXXXXXXXXXXXXX/info_in/target`

Topic slouží k zjištění typu desky, se kterou Homer komunikuje.

Seznam targetů je možné nalézt na [přehledu targetů](https://wiki.byzance.cz/wiki/doku.php?id=specs:targetlist).

**Request:**

```
 {
   "mid"            : "SOME ID"
 }
```

**Reply:**

```
 {
   "mid"            : "SOME ID"
   "status"         : "ok/error",
   "error"          : "SOME ERROR MESSAGE", // pouze pokud je status == error
   "error_code"     :  SOME NUMBER,         // pouze pokud je status == error
   "target"         : "SOME VALUE"          // pouze pokud je status == ok
 }
```

### Informace o "cpuload"

Přistupuje se do něj takto`XXXXXXXXXXXXXXXXXXXXXXXX/info_in/cpuload`

Topic slouží k zjištění využití proceosoru v zařízení. Cpuload je orientační číslo 0-100. Více informací viz článek[CPU load](https://wiki.byzance.cz/wiki/doku.php?id=feature:cpuload)

**Request:**

```
 {
   "mid"            : "SOME ID"
 }
```

**Reply:**

```
{
   "mid"            : "SOME ID"
   "status"         : "ok/error",
   "error"          : "SOME ERROR MESSAGE", // pouze pokud je status == error
   "error_code"     :  SOME NUMBER,         // pouze pokud je status == error
   "cpuload"        :  SOME NUMBER 0-100    // pouze pokud je status == ok
 }
```



### Informace o "version"

Přistupuje se do něj takto`XXXXXXXXXXXXXXXXXXXXXXXX/info_in/version`

Topic slouží k zjištění verze určité komponenty.

U Yody jsou validní 4 komponenty:`firmware`,`bootloader`,`backup`,`buffer`.

**Request:**

```
 {
   "mid"            : "SOME ID"
   "component"      : "SOME COMPONENT"
 }
```

**Reply:**

```
 {
   "mid"            : "SOME ID"
   "status"         : "ok/error",
   "error"          : "SOME ERROR MESSAGE", // pouze pokud je status == error
   "error_code"     :  SOME NUMBER,         // pouze pokud je status == error
   "component"      : "SOME COMPONENT"      // pouze pokud je status == ok
   "size"           :  SOME NUMBER,         // pouze pokud je status == ok
   "crc"            :  SOME NUMBER,         // pouze pokud je status == ok
   "build_id"       : "SOME BUILD_ID",      // pouze pokud je status == ok
   "version"        : "SOME VALUE",         // pouze pokud je status == ok  
   "timestamp"      :  SOME NUMBER,         // pouze pokud je status == ok
   "usr_version"    : "SOME VALUE",         // pouze pokud je status == ok  
   "usr_name"       : "SOME VALUE",         // pouze pokud je status == ok  
   "name"           : "SOME NAME"           // pouze pokud je status == ok
 }
```

### Informace o "alias"

Přistupuje se do něj takto`XXXXXXXXXXXXXXXXXXXXXXXX/info_in/mac`

Topic slouží k zjištění mac adres jednotlivých komponent. Více informací v článku o[ethernetu](https://wiki.byzance.cz/wiki/doku.php?id=feature:ethernet).

**Request:**

```
{
   "mid"            : "SOME ID"
 }
```

**Reply:**

```
 {
   "mid"            : "SOME ID"
   "status"         : "ok/error",
   "error"          : "SOME ERROR MESSAGE", // pouze pokud je status == error
   "error_code"     :  SOME NUMBER,         // pouze pokud je status == error
   "mac-eth"        : "SOME VALUE"          // pouze pokud je status == ok
   "mac-wifi"       : "SOME VALUE"          // pouze pokud je status == ok
 }
```

### Informace o "ip"

Přistupuje se do něj takto`XXXXXXXXXXXXXXXXXXXXXXXX/info_in/ip`

Topic slouží k zjištění ip adresy Yody. Více informací v článku o[ethernetu](https://wiki.byzance.cz/wiki/doku.php?id=feature:ethernet).

**Request:**

```
 {
   "mid"            : "SOME ID"
 }
```

**Reply:**

```
 {
   "mid"            : "SOME ID"
   "status"         : "ok/error",
   "error"          : "SOME ERROR MESSAGE", // pouze pokud je status == error
   "error_code"     :  SOME NUMBER,         // pouze pokud je status == error
   "ip"             : "SOME VALUE"          // pouze pokud je status == ok
 }
```

### Infromace o "memsize"

Přistupuje se do něj takto`XXXXXXXXXXXXXXXXXXXXXXXX/info_in/memsize`

Topic slouží k zjištění velikosti vnitřní paměti zařízení. Čísla jsou v bytech. Více informací v článku o[Interní paměťi mikrokontroléru](https://wiki.byzance.cz/wiki/doku.php?id=memory:internal).

**Request:**

```
{
   "mid"            : "SOME ID"
 }
```

**Reply:**

```
 {
   "mid"            : "SOME ID"
   "status"         : "ok/error",
   "error"          : "SOME ERROR MESSAGE", // pouze pokud je status == error
   "error_code"     :  SOME NUMBER,         // pouze pokud je status == error
   "bootloader"     :  SOME NUMBER,         // pouze pro status == ok + YODAG2, WRLSKITG2 nebo BUSKITG2
   "firmware"       :  SOME NUMBER,         // pouze pro status == ok + YODAG2, WRLSKITG2 nebo BUSKITG2
   "buffer"         :  SOME NUMBER          // pouze pro status == ok + YODAG2
 }
```

### Informace o "datetime"

Přistupuje se do něj takto`XXXXXXXXXXXXXXXXXXXXXXXX/info_in/datetime`

Topic slouží k zjištění aktuálního času z hodin, které má v sobě Yoda. Čas je klasické unix timestamp. Více informací v článku o[Práce s datem a časem \(RTC\)](https://wiki.byzance.cz/wiki/doku.php?id=tutorial:timestamp).

**Request:**

```
 {
   "mid"            : "SOME ID"
 }
```

**Reply:**

```
 {
   "mid"            : "SOME ID"
   "status"         : "ok/error",
   "error"          : "SOME ERROR MESSAGE", // pouze pokud je status == error
   "error_code"     :  SOME NUMBER,         // pouze pokud je status == error   
   "datetime"       :  SOME NUMBER          // pouze pokud je status == ok
 }
```

### Informace o "timesync"

Přistupuje se do něj takto`XXXXXXXXXXXXXXXXXXXXXXXX/info_in/timesync`

Topic slouží k zjištění, jestli je synchronizace času se serverem zapnutá, nebo ne. Více informací v článku o [Práce s datem a časem \(RTC\)](https://wiki.byzance.cz/wiki/doku.php?id=tutorial:timestamp).

**Request:**

```
 {
   "mid"            : "SOME ID"
 }
```

**Reply:**

```
 {
   "mid"            : "SOME ID"
   "status"         : "ok/error",
   "error"          : "SOME ERROR MESSAGE", // pouze pokud je status == error
   "error_code"     :  SOME NUMBER,         // pouze pokud je status == error   
   "timesync"       :  true/false           // pouze pokud je status == ok
 }
```

### Informace o "uptime"

Přistupuje se do něj takto`XXXXXXXXXXXXXXXXXXXXXXXX/info_in/uptime`

Topic slouží k zjištění toho, jak dlouho zařízení běží. Při startu zařížení má čítač hodnotu 0, každou sekundu se inkrementuje až do hodnoty 2^32 - 1, tj. 4 294 967 295, což odpovídá cca 136 let. Více informací viz článek[Uptime](https://wiki.byzance.cz/wiki/doku.php?id=feature:uptime)

**Request:**

```
 {
   "mid"            : "SOME ID"
 }
```

**Reply:**

```
 {
   "mid"            : "SOME ID"
   "status"         : "ok/error",
   "error"          : "SOME ERROR MESSAGE", // pouze pokud je status == error
   "error_code"     :  SOME NUMBER,         // pouze pokud je status == error   
   "device_counter" :  SOME NUMBER          // pouze pokud je status == ok
 }
```

### Informace o  "autobackup"

Přistupuje se do něj takto`XXXXXXXXXXXXXXXXXXXXXXXX/info_in/autobackup`

Topic slouží k zjištění stavu funkce autobackup. Funkce automaticky před nahráním nového firmware v bootloaderu zazálohuje aktuální. V případě, že je v zařízení nastaven nějaký defaultní firmware, je přepsám. Více informací v článku o[Autobackup](https://wiki.byzance.cz/wiki/doku.php?id=feature:autobackup).

**Request:**

```
 {
   "mid"            : "SOME ID"
 }
```

**Reply:**

```
 {
   "mid"            : "SOME ID"
   "status"         : "ok/error",
   "error"          : "SOME ERROR MESSAGE", // pouze pokud je status == error
   "error_code"     :  SOME NUMBER,         // pouze pokud je status == error   
   "autobackup"     :  true/false           // pouze pokud je status == ok
 }
```

### Informace o "state"

Přistupuje se do něj takto`XXXXXXXXXXXXXXXXXXXXXXXX/info_in/state`

Topic slouží k zjištění stavu jednotlivých komponent yody. Více informací v článku o [State](https://wiki.byzance.cz/wiki/doku.php?id=feature:state)

**Request:**

```
 {
   "mid"            : "SOME ID"
 }
```

**Reply:**

```
 {
   "mid"            : "SOME ID",
   "buffer"         : "invalid/valid/erasing/erased",
   "backup"         : "invalid/valid/erasing/erased",
   "error"          : "SOME ERROR MESSAGE",   // pouze pokud je status == error
   "error_code"     :  SOME NUMBER,           // pouze pokud je status == error  
 }
```

### Informace o "normal\_mqtt\_connection"

Přistupuje se do něj takto`XXXXXXXXXXXXXXXXXXXXXXXX/info_in/normal_mqtt_connection`

Zjištění aktuálního normal\_mqtt\_connection, který byl nastavený v topicu`XXXXXXXXXXXXXXXXXXXXXXXX/settings_in/normal_mqtt_connection`. Více informací v článku o[MQTT komunikace](https://wiki.byzance.cz/wiki/doku.php?id=yoda:mqtt).

**Request:**

```
 {
   "mid"            : "SOME ID"
 }
```

**Reply:**

```
 {
   "mid"            : "SOME ID"
   "status"         : "ok/error",
   "error"          : "SOME ERROR MESSAGE", // pouze pokud je status == error
   "error_code"     :  SOME NUMBER,         // pouze pokud je status == error   
   "connection"     : "SOME VALUE"          // pouze pokud je status == ok
 }
```

### Informace o "backup\_mqtt\_connection"

Přistupuje se do něj takto`XXXXXXXXXXXXXXXXXXXXXXXX/info_in/backup_mqtt_connection`

Zjištění aktuálního backup\_mqtt\_connection, který byl nastavený v topicu`XXXXXXXXXXXXXXXXXXXXXXXX/settings_in/backup_mqtt_connection`. Více informací v článku o[MQTT komunikace](https://wiki.byzance.cz/wiki/doku.php?id=yoda:mqtt).

**Request:**

```
 {
   "mid"            : "SOME ID"
 }
```

**Reply:**

```
 {
   "mid"            : "SOME ID"
   "status"         : "ok/error",
   "error"          : "SOME ERROR MESSAGE", // pouze pokud je status == error
   "error_code"     :  SOME NUMBER,         // pouze pokud je status == error   
   "connection"     : "SOME VALUE"          // pouze pokud je status == ok
 }
```

### Informace o "wifi"

Přistupuje se do něj takto`XXXXXXXXXXXXXXXXXXXXXXXX/info_in/wifi_ssid`

Zjištění aktuálního wifi\_ssid, který byl nastavený v topicu`XXXXXXXXXXXXXXXXXXXXXXXX/settings_in/wifi_ssid`.

Wifi SSID by se mělo dát nastavit, pokud je Yoda nakonfigurovaný jako wifi host. Potom se přepne jako wifi klient.

Tento příkaz má smysl pouze při připojení kabelem. Více informací v článku o[wifi](https://wiki.byzance.cz/wiki/doku.php?id=feature:wifi).

**Request:**

```
 {
   "mid"            : "SOME ID"
 }
```

**Reply:**

```
 {
   "mid"            : "SOME ID"
   "status"         : "ok/error",
   "error"          : "SOME ERROR MESSAGE", // pouze pokud je status == error
   "error_code"     :  SOME NUMBER,         // pouze pokud je status == error   
   "firmware"       : "SOME VALUE"          // pouze pokud je status == ok
   "mac"            : "SOME VALUE"          // pouze pokud je status == ok
   "espid"          :  SOME NUMBER          // pouze pokud je status == ok
   "flashid"        :  SOME NUMBER          // pouze pokud je status == ok
   "flashsize"      :  SOME NUMBER          // pouze pokud je status == ok
   "flashspeed"     :  SOME NUMBER          // pouze pokud je status == ok
 }
```
### Informace o "wifi_ssid" 

Přistupuje se do něj takto
''XXXXXXXXXXXXXXXXXXXXXXXX/info_in/wifi_ssid''

Zjištění aktuálního wifi_ssid, který byl nastavený v topicu ''XXXXXXXXXXXXXXXXXXXXXXXX/settings_in/wifi_ssid''.

Wifi SSID by se mělo dát nastavit, pokud je Yoda nakonfigurovaný jako wifi host. Potom se přepne jako wifi klient.

Tento příkaz má smysl pouze při připojení kabelem. Více informací v článku o [[feature:wifi|wifi]].

**Request:**
```
 {
   "mid"            : "SOME ID"
 }
```
**Reply:**
```
 {
   "mid"            : "SOME ID"
   "status"         : "ok/error",
   "error"          : "SOME ERROR MESSAGE", // pouze pokud je status == error
   "error_code"     :  SOME NUMBER,         // pouze pokud je status == error   
   "ssid"           : "SOME VALUE"          // pouze pokud je status == ok
 }
```

### Informace o "wifi_password" 

Přistupuje se do něj takto
''XXXXXXXXXXXXXXXXXXXXXXXX/info_in/wifi_password''

Zjištění aktuálního wifi_password, který byl nastavený v topicu ''XXXXXXXXXXXXXXXXXXXXXXXX/settings_in/wifi_password''. Více informací v článku o [[feature:wifi|wifi]].

**Request:**
```
 {
   "mid"            : "SOME ID"
 }
```
**Reply:**
```
 {
   "mid"            : "SOME ID"
   "status"         : "ok/error",
   "error"          : "SOME ERROR MESSAGE", // pouze pokud je status == error
   "error_code"     :  SOME NUMBER,         // pouze pokud je status == error   
   "password"       : "SOME VALUE"          // pouze pokud je status == ok
 }
```

### Informace o "console" 

Přistupuje se do něj takto
''XXXXXXXXXXXXXXXXXXXXXXXX/info_in/console''

Zjištění aktuálního stavu console, který byl nastavený v topicu ''XXXXXXXXXXXXXXXXXXXXXXXX/settings_in/console''. Více informací v článku o [[tutorial:console|Webová konzole]].

**Request:**
```
 {
   "mid"            : "SOME ID"
 }
```
**Reply:**
```
 {
   "mid"            : "SOME ID"
   "status"         : "ok/error",
   "error"          : "SOME ERROR MESSAGE", // pouze pokud je status == error
   "error_code"     :  SOME NUMBER,         // pouze pokud je status == error   
   "console"        :  TRUE/FALSE           // pouze pokud je status == ok
 }
```
### Informace o "webview" 

Přistupuje se do něj takto
''XXXXXXXXXXXXXXXXXXXXXXXX/info_in/webview''

Zjištění, jestli je funkce webview zapnutá, což mohlo nastat v topicu ''XXXXXXXXXXXXXXXXXXXXXXXX/settings_in/webview''. Více informací v článku o [[tutorial:webview|Webové rozhraní]].

**Request:**
```
 {
   "mid"            : "SOME ID"
 }
```
**Reply:**
```
 {
   "mid"            : "SOME ID"
   "status"         : "ok/error",
   "error"          : "SOME ERROR MESSAGE", // pouze pokud je status == error
   "error_code"     :  SOME NUMBER,         // pouze pokud je status == error   
   "webview"        :  TRUE/FALSE           // pouze pokud je status == ok
 }
```

### Informace o "webport" 

Přistupuje se do něj takto
''XXXXXXXXXXXXXXXXXXXXXXXX/info_in/webport''

Zjištění aktuálního portu, na kterém bude nabíhat webview, přičemž port byl nastaven v topicu ''XXXXXXXXXXXXXXXXXXXXXXXX/settings_in/webport''.  Více informací v článku o [[tutorial:webview|Webové rozhraní]].

**Request:**
```
 {
   "mid"            : "SOME ID"
 }
```
**Reply:**
```
 {
   "mid"            : "SOME ID"
   "status"         : "ok/error",
   "error"          : "SOME ERROR MESSAGE", // pouze pokud je status == error
   "error_code"     :  SOME NUMBER,         // pouze pokud je status == error   
   "webport"        :  SOME NUMBER          // pouze pokud je status == ok
 }
```

### Informace o "revision" 

Přistupuje se do něj takto
''XXXXXXXXXXXXXXXXXXXXXXXX/info_in/revision''

Zjištění aktuálního čísla revize. Položka je read-only a není možné ji nastavit žádným [[yoda:topic_settings|settings topicem]].
 Více informací v článku o [[feature:revision|Revision]].

**Request:**
```
 {
   "mid"            : "SOME ID"
 }
```
**Reply:**
```
 {
   "mid"            : "SOME ID"
   "status"         : "ok/error",
   "error"          : "SOME ERROR MESSAGE", // pouze pokud je status == error
   "error_code"     :  SOME NUMBER,         // pouze pokud je status == error   
   "revision"       : "SOME REVISION"       // pouze pokud je status == ok
 }
```


### Chybové stavy 

Každý příkaz může selhat s určitým chybovým kódem. Seznam takovýchto chybových kódů je v [[errorcodes:errorcodes|přehledu chybových kódů]].



