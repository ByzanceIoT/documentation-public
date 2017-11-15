# Mqtt Topic settings

Topic slouží k nastavování různých parametrů yody. Komunikuje se pomocí JSONů, které mají přesně dané parametry.

JSON z Homera do Yody má 2 povinné labely, které vypadají takto:

**Request**:

```
 {
   "mid"            : "SOME ID",
   "value"          : "SOME VALUE" // někdy je to string, někdy integer, někdy boolen - viz dokumentace
 }
```

V labelu`mid`je nějaké ID zprávy, které generuje Homer Yodovi. Yoda mu stejné`mid`vrací zpátky.

V labelu „value“ je určitá hodnota prvku, který chce Homer v Yodovi nastavit. Prvek je získán z příslušného subtopicu, do kterého byl JSON poslán.

Pokud nastavení proběhne v pořádku, v odpovědi se vytvoří label „status“, který může nabývat hodnot „ok“ nebo „error“.

* Pokud label „status“ nabývá hodnoty „error“, vytvoří se nový label „error“, v němž je popis chyby, která nastala.
* Pokud label „status“ nabývá hodnoty „ok“, zkopíruje se label „value“ pro kontrolu zpátky.

Pokud je třeba zjistit hodnotu některé už nastavené položky, je třeba to zjistit v odpovídající položce přes topic [MQTT Topic Info](https://wiki.byzance.cz/wiki/doku.php?id=yoda:topic_info)

## Subtopic "alias"

Přistupuje se do něj takto`XXXXXXXXXXXXXXXXXXXXXXXX/settings_in/alias`

Pokud je třeba zjistit už nastavenou hodnotu, je třeba poslat dotaz do topicu[MQTT Topic Info](https://wiki.byzance.cz/wiki/doku.php?id=yoda:topic_info)`XXXXXXXXXXXXXXXXXXXXXXXX/info_in/alias`

Topic slouží k nastavení aliasu zařízení. Alias je lidsky čitelnýASCIIstring. Více informací v článku[o alias](https://wiki.byzance.cz/wiki/doku.php?id=feature:alias).

**Request:**

```
 {
   "mid"            : "SOME ID",
   "value"          : "SOME ALIAS"
 }
```

**Reply:**

```
 {
   "mid"            : "SOME ID",
   "status"         : "ok/error",
   "error"          : "SOME ERROR MESSAGE", // pouze pokud je status == error
   "error_code"     :  SOME NUMBER,         // pouze pokud je status == error
   "value"          : "SOME ALIAS"          // pouze pokud je status == ok
 }
```

## Subtopic "datetime" {#subtopic_datetime}

Přistupuje se do něj takto`XXXXXXXXXXXXXXXXXXXXXXXX/settings_in/datetime`

Pokud je třeba zjistit už nastavenou hodnotu, je třeba poslat dotaz do topicu [MQTT Topic Info](https://wiki.byzance.cz/wiki/doku.php?id=yoda:topic_info)`XXXXXXXXXXXXXXXXXXXXXXXX/info_in/datetime`

Topic slouží k nastavení hodin v Yodovi. Používá se klasický unixový timestamp.

Požadavek přímo přes konzoli v Homerovi takto

```
sendJson i1 settings_in/datetime '{"value": 1471016024}'
```

**Request:**

```
 {
   "mid"            : "SOME ID",
   "value"          :  SOME NUMBER
 }
```

**Reply:**

```
 {
   "mid"            : "SOME ID",
   "status"         : "ok/error",
   "error"          : "SOME ERROR MESSAGE", // pouze pokud je status == error
   "error_code"     :  SOME NUMBER,         // pouze pokud je status == error
   "value"          :  SOME NUMBER          // pouze pokud je status == ok
 }
```

## Subtopic "timesync"

Přistupuje se do něj takto`XXXXXXXXXXXXXXXXXXXXXXXX/settings_in/timesync`

Pokud je třeba zjistit už nastavenou hodnotu, je třeba poslat dotaz do topicu[MQTT Topic Info](https://wiki.byzance.cz/wiki/doku.php?id=yoda:topic_info)`XXXXXXXXXXXXXXXXXXXXXXXX/info_in/timesync`

Topic slouží k zapnutí nebo vypnutí synchronizace času Iody s Homerem.

**Request:**

```
 {
   "mid"            : "SOME ID",
   "value"          :  true/false
 }
```

**Reply:**

```
 {
   "mid"            : "SOME ID",
   "status"         : "ok/error",
   "error"          : "SOME ERROR MESSAGE", // pouze pokud je status == error
   "error_code"     :  SOME NUMBER,         // pouze pokud je status == error
   "value"          :  true/false           // pouze pokud je status == ok
 }
```

## Subtopic "autobackup"

Přistupuje se do něj takto`XXXXXXXXXXXXXXXXXXXXXXXX/settings_in/autobackup`

Pokud je třeba zjistit už nastavenou hodnotu, je třeba poslat dotaz do topicu[MQTT Topic Info](https://wiki.byzance.cz/wiki/doku.php?id=yoda:topic_info)`XXXXXXXXXXXXXXXXXXXXXXXX/info_in/autobackup`

Topic slouží k zapnutí nebo vypnutí funkce autobackup. Funkce automaticky před nahráním nového firmware v bootloaderu zazálohuje aktuální. V případě, že je v zařízení nastaven nějaký defaultní firmware, je přepsán. Více informací v článku[o autobackup](https://wiki.byzance.cz/wiki/doku.php?id=feature:autobackup).

**Request:**

```
 {
   "mid"            : "SOME ID",
   "value"          :  true/false
 }
```

**Reply:**

```
 {
   "mid"            : "SOME ID",
   "status"         : "ok/error",
   "error"          : "SOME ERROR MESSAGE", // pouze pokud je status == error
   "error_code"     :  SOME NUMBER,         // pouze pokud je status == error   
   "value"          : "SOME VALUE"          // pouze pokud je status == ok
 }
```

## Subtipic "backup\_mqtt\_connection"

Přistupuje se do něj takto`XXXXXXXXXXXXXXXXXXXXXXXX/settings_in/backup_mqtt_connection`

Pokud je třeba zjistit už nastavenou hodnotu, je třeba poslat dotaz do topicu[MQTT Topic Info](https://wiki.byzance.cz/wiki/doku.php?id=yoda:topic_info)`XXXXXXXXXXXXXXXXXXXXXXXX/info_in/backup_mqtt_connection`

Příkaz slouží k nastavení záložní IP adresy a portu, na které se bude Homer připojovat.

**Request:**

```
{
   "mid"            : "SOME ID",
   "value"          : "192.168.065.179:1881"
 }
```

**Reply:**

```
 {
   "mid"            : "SOME ID",
   "status"         : "ok/error",
   "error"          : "SOME ERROR MESSAGE", // pouze pokud je status == error
   "error_code"     :  SOME NUMBER,         // pouze pokud je status == error   
   "value"          : "SOME VALUE"          // pouze pokud je status == ok
 }
```

## Subtopic "wifi\_username"

Přistupuje se do něj takto`XXXXXXXXXXXXXXXXXXXXXXXX/settings_in/wifi_username`

Pokud je třeba zjistit už nastavenou hodnotu, je třeba poslat dotaz do topicu[MQTT Topic Info](https://wiki.byzance.cz/wiki/doku.php?id=yoda:topic_info)`XXXXXXXXXXXXXXXXXXXXXXXX/info_in/wifi_username`

Příkaz slouží k nastavení uživatelského jména do[wifi](https://wiki.byzance.cz/wiki/doku.php?id=feature:wifi).

**Request:**

```
 {
   "mid"            : "SOME ID",
   "value"          : "username"
 }
```

**Reply:**

```
{
   "mid"            : "SOME ID",
   "status"         : "ok/error",
   "error"          : "SOME ERROR MESSAGE", // pouze pokud je status == error
   "error_code"     :  SOME NUMBER,         // pouze pokud je status == error   
   "value"          : "SOME VALUE"          // pouze pokud je status == ok
 }
```

## Subtopic "console"

Přistupuje se do něj takto`XXXXXXXXXXXXXXXXXXXXXXXX/settings_in/console`

Pokud je třeba zjistit už nastavenou hodnotu, je třeba poslat dotaz do topicu[MQTT Topic Info](https://wiki.byzance.cz/wiki/doku.php?id=yoda:topic_info)`XXXXXXXXXXXXXXXXXXXXXXXX/info_in/console`

Příkaz slouží k zapnutí nebo vypnutí[webové console](https://wiki.byzance.cz/wiki/doku.php?id=tutorial:console).

**Request:**

```
 {
   "mid"            : "SOME ID",
   "value"          : TRUE/FALSE
 }
```

**Reply:**

```
 {
   "mid"            : "SOME ID",
   "status"         : "ok/error",
   "error"          : "SOME ERROR MESSAGE", // pouze pokud je status == error
   "error_code"     :  SOME NUMBER,         // pouze pokud je status == error   
   "value"          :  TRUE/FALSE          // pouze pokud je status == ok
 }
```

## Subtopic "webview"

Přistupuje se do něj takto`XXXXXXXXXXXXXXXXXXXXXXXX/settings_in/webview`

Pokud je třeba zjistit už nastavenou hodnotu, je třeba poslat dotaz do topicu[MQTT Topic Info](https://wiki.byzance.cz/wiki/doku.php?id=yoda:topic_info)`XXXXXXXXXXXXXXXXXXXXXXXX/info_in/webview`

Příkaz slouží k zapnutí nebo vypnutí[webového rozhraní](https://wiki.byzance.cz/wiki/doku.php?id=tutorial:webview).

**Request:**

```
 {
   "mid"            : "SOME ID",
   "value"          : TRUE/FALSE
 }
```

**Reply:**

```
 {
   "mid"            : "SOME ID",
   "status"         : "ok/error",
   "error"          : "SOME ERROR MESSAGE", // pouze pokud je status == error
   "error_code"     :  SOME NUMBER,         // pouze pokud je status == error   
   "value"          :  TRUE/FALSE          // pouze pokud je status == ok
 }
```

## Subtopic "webport"

Přistupuje se do něj takto`XXXXXXXXXXXXXXXXXXXXXXXX/settings_in/webport`

Pokud je třeba zjistit už nastavenou hodnotu, je třeba poslat dotaz do topicu[MQTT Topic Info](https://wiki.byzance.cz/wiki/doku.php?id=yoda:topic_info)`XXXXXXXXXXXXXXXXXXXXXXXX/info_in/webport`

Příkaz slouží k nastavení portu pro[webové rozhraní](https://wiki.byzance.cz/wiki/doku.php?id=tutorial:webview).

**Request:**

```
 {
   "mid"            : "SOME ID",
   "value"          :  SOME NUMBER
 }
```

**Reply:**

```
{
   "mid"            : "SOME ID",
   "status"         : "ok/error",
   "error"          : "SOME ERROR MESSAGE", // pouze pokud je status == error
   "error_code"     :  SOME NUMBER,         // pouze pokud je status == error   
   "value"          :  SOME NUMBER          // pouze pokud je status == ok
 }
```

## Subtopic "blreport"

TO DO

## Subtopic "wdenable"

TO DO

## Subtopic "wdtime" 

TO DO

## Subtopic "backuptime"

TO DO

## Subtopic "timeoffset"

TO DO 
## Subtopic "lowpanbr"

TO DO

## Subtopic "autojump"

TO DO

## Chybové stavy: {#chybove_stavy}

Každý příkaz může selhat s určitým chybovým kódem. Seznam takovýchto chybových kódů je v

[přehledu chybových kódů](https://wiki.byzance.cz/wiki/doku.php?id=errorcodes:errorcodes)



