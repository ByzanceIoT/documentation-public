## MQTT Topic Commands

Další možné topicy jsou \[\[Yoda:topic\_settings\|settings\]\] a \[\[Yoda:topic\_info\|info\]\]

#### Subtopic "upload"

Příkazy pro část "upload" v procesu \[\[Yoda:aktualizace\_firmware\|aktualizace firmware\]\]. Pomocí následujích 3 příkazů se do Yody dá nahrát binárka k určité komponentě firmware.

#### Subtopic "start" ====

Přistupuje se do něj takto

''XXXXXXXXXXXXXXXXXXXXXXXX/command\_in/upload/start''

Polozka ''"name"'' obsahuje volitelny textovy popisek \(napr. ve zkratce, co dany program dela - je to uzivatelska informace\). Maximalni delka je 64B včetně ukončovacího znaku.

Položka ''"buildId"'' ma rovněž maximálně 64 znaků.

Položka ''"version"'' se sklada ze čtyř části: \*\*jeden\*\* znak \(písmeno\) a pak tři čísla v rozmezí 0-255. Oddělovačem je \*\*povinně\*\* tečka. Jinými slovy každá ze čtyř části se ukládá do proměnné o velikosti 1B a proto nelze uložit jiné hodnoty. \*\*Neplatné\*\* jsou verze jako "VER0.0.0", "V0.278.0", "AB1580" nebo "V1.01". Sparvne jsou verze "a0.0.0" až "Z255.255.255".

Odpověď na příkaz přijde okamžitě, nicméně to neznamená, že je Yoda připraven binárku přijmout. Je třeba potom kouknout na stav jednotlivých vnitřních komponent, jestli jsou OK.

**Request:**

```
"mid"            : "SOME ID",
"size"           :  SIZE OF WHOLE BINARY FILE BEFORE BASE64,
"crc"            :  CHECKSUM OF WHOLE BINARY FILE BEFORE BASE64,
"buildId"        : "SOME BUILD_ID - UUID 36 Chars", (No space allowed) (47 char max)
"version"        : "v0.0.0" || "v0.0.1-beta" "v99.99.99-alpha.9" (whole version 31 char max)
"timestamp"      :  UNIX TIMESTAMP, (zatim nepovinne)
"usr_version"    : "v0.0.0", (zatim nepovinne) ( User set this name) For Example  "1.0...2" or "Last try for this shit" (31 char max)
"usr_name"       : "rychle_blikani_ledkou", (zatim nepovinne) (31 char max)
}
```

**Reply:**

```
{
"mid"            : "SOME ID",
"status"         : "ok/error",
"error"          : "SOME ERROR MESSAGE", // pouze pokud je status == error
"error_code"     :  SOME NUMBER          // pouze pokud je status == error
}
```

#### Subtopic "end"

Přistupuje se do něj takto

''XXXXXXXXXXXXXXXXXXXXXXXX/command\_in/upload/end''

\*\*Request:\*\*

```
{
"mid"            : "SOME ID"
}
```

**Reply:**

```
{
"mid"            : "SOME ID",
"status"         : "ok/error",
"error"          : "SOME ERROR MESSAGE", // pouze pokud je status == error
"error_code"     :  SOME NUMBER          // pouze pokud je status == error
}
```

#### Subtopic "data"

Přistupuje se do něj takto

''XXXXXXXXXXXXXXXXXXXXXXXX/command\_in/upload/data''

**Request:**

```
{
"mid"            : "SOME ID",
"part"           :  SOME NUMBER,
"crc"            :  SOME CRC OF FOLLOWING PART OF DATA BEFORE BASE64,
"size"           :  768 BYTES (BEFORE BASE64)
"data"           : "BINARY DATA WITH SIZE DEFINED IN LABEL "size",
}
```

**Reply:**

```
{
"mid"            : "SOME ID",
"status"         : "ok/error",
"error"          : "SOME ERROR MESSAGE", // pouze pokud je status == error
"error_code"     :  SOME NUMBER          // pouze pokud je status == error
}
```

#### Subtopic "update"

Jelikož jsme se dohodli že Homer nemusí rozumět tomu jaké zařízení updatuje. Což je důležité do budoucna.

Ale update Yody trvá "hned" update devicu i 3 minuty.... Proto je tu důležitý další parametr. Existují dva různe topicy: topic ''start'' a topic ''status''.

#### Subsubtopic "start"

Přistupuje se do něj takto

''XXXXXXXXXXXXXXXXXXXXXXXX/command\_in/update/start''

Příkazy pro část "update" v procesu \[\[Yoda:aktualizace\_firmware\|aktualizace firmware\]\]. Stručně řečeno, jeho smyslem je odstartovat samotný proces přepisu FLASH paměti aktualizovaného zařízení.

Význam tohoto topicu podle typu zařízení a typu binárky:

* U **Iody**:

```
\* \*\*firmware\*\* - zapsani flagu na update do FLASh paměti, pak čekani na restart od Homera

\* \*\*bootloader\*\* - přepis oblasti bootloaderu v interni paměti mikrokontroleru novým bootloaderem, pak čekání na restart

\* \*\* backup\*\* - přepis oblasti s komponentou backup
```

**Request:**

```
{
"mid"            : "SOME ID",
"component"      : "firmware/bootloader/backup"
}
```

**Reply:**

```
{
"mid"            : "SOME ID",
"status"         : "ok/error",
"error"          : "SOME ERROR MESSAGE", // pouze pokud je status == error
"error_code"     :  SOME NUMBER          // pouze pokud je status == error
}
```

#### Subtopic "status"

Přistupuje se do něj takto

''XXXXXXXXXXXXXXXXXXXXXXXX/command\_in/update/status''

Topic platný pouze v případě, že jde o  ''"update\_state"   : "longTerm"'' typ nahrávání firmwaru, tj. přenos binárky z Yody na Device, který je časově náročnější. Homer se dotazuje na progress updatu, kde chce znát procentuální stav nahrávání. \(Homer se ptá, Yoda odpovídá\)

**Request:**

```
{
"mid"            : "SOME ID",
"device"         : "FULL ID DEVICE, kterého aktuálně Yoda updatuje"
}
```

**Reply:**

```
{
"mid"            : "SAME ID",
"status"         : "ok/error",
"progress"       : 14   <----- int číslo, od 0 do 100 zastupující % update
"error"          : "SOME ERROR MESSAGE", // pouze pokud je status == error
"error_code"     :  SOME NUMBER          // pouze pokud je status == error
}
```

#### Subtopic "device"

Subtopic slouží k práci se seznamem zařízení, se kterými bude Yoda komunikovat.

#### Subtopic "add"

Přistupuje se do něj takto

''XXXXXXXXXXXXXXXXXXXXXXXX/command\_in/device/add''

Slouží k přidání nového zařízení do Yody. \*\*Pokud už zařízení už v yodovi existuje, návratový JSON obsahuje status "ok", a result "existing". Pokud zařízení neexistuje, status="ok" a result="new". Result "error" může nastat pouze v případě, že se něco vyloženě pokazí\*\*.

**Request:**

```
{
"mid"           : "SOME ID",
"deviceId"      : "24 BYTES OF FULL ID"
}
```

**Reply:**

```
{
"mid"            : "SOME ID",
"status"         : "ok/error",
"error"          : "SOME ERROR MESSAGE", // pouze pokud je status == error
"error_code"     :  SOME NUMBER,         // pouze pokud je status == error
"result"         : "new/existing"        // pouze pokud je status == ok
}
```

#### Subtopic "remove"

Přistupuje se do něj takto

''XXXXXXXXXXXXXXXXXXXXXXXX/command\_in/device/remove''

Slouží k odebrání zařízení z Yody pro potřeby Homera. Reálny vliv je takový, že device \*\*není\*\* ze seznamu zařízení smazán, ale je mu nastaven status ''saved'' na ''false'' a také je jeho ''state'' na ''DISCONNECTED'' \(číselně ''0x01''\).

**Request:**

```
{
"mid"              : "SOME ID",
"deviceId"         : "24 BYTES FULL ID" (Index není podporován ze strany homera!! Homer neumí pořadí pole!
}
```

**Reply:**

```
{
"mid"            : "SOME ID",
"status"         : "ok/error",
"error"          : "SOME ERROR MESSAGE", // pouze pokud je status == error
"error_code"     :  SOME NUMBER,         // pouze pokud je status == error
"result"         : "removed/missing"     // pouze pokud je status == ok
}
```

#### Subtopic "get"

Přistupuje se do něj takto

''XXXXXXXXXXXXXXXXXXXXXXXX/command\_in/device/get''

Pokud zařízení není saved, snažilo se připojit k Yodovi a existuje v síti.

Yoda se s ním ale nebaví, dokud nedostane pokyn.

interface, state:

odpovídá ItfEnum\_TypeDef a StateEnum\_TypeDef v souboru DevList.h

Pokud zařízení není reálně připojeno, jeho interface je unknown. Až se připojí, interface se přiřadí na aktuální hodnotu.



```
typedef enum ( Typy zařízení - jako je drátový nebo bezdrátový)
{
ITF_UNKNOWN   = 0x00,
ITF_NRF       = 0x01, (Bezdrát)
ITF_RS485     = 0x02, (Drát)
ITF_ERROR     = 0xFF
} ItfEnum_TypeDef;
```

```
typedef enum : unsigned char {
DEV\_STATE\_UNKNOWN        = 0x00, // Device zatim nema nastaveny zadny stav, tj po startu.

DEV\_STATE\_DISCONNECTED            = 0x01, // Device je odpojeno - Homer si s nim nechce povidat.

DEV\_STATE\_ADD            = 0x02, // Device se bude enumerovat \(prechodny stav\), Yoda poslal prikaz add.

DEV\_STATE\_ALIVE          = 0x03, // Enumerace probiha \(prechodny stav\).

DEV\_STATE\_ENUMERATED            = 0x04,    // Je enumerovano a normalne zije a komunikuje.

DEV\_STATE\_REMOVE        = 0x05,    // Device se ma zakazat \(prechodny stav\), Yoda poslal prikaz remove.

DEV\_STATE\_TIMEOUT        = 0x14, // Nekolikrat neodpovedelo, ale jeste neni prohlaseno za mrtve. \(20 dekadické\) 

DEV\_STATE\_DEAD            = 0x15, // Prohlaseno za mrtve - neodpovida. \(21 dekadické\)

DEV\_STATE\_ERROR            = 0x20    // error \(32 dekadické\)
} StateEnum_TypeDef;
```



**Request:**

```
{
"mid"             : "SOME ID",
// Json musí obsahova buď "deviceId" nebo "device_count" - nic jiného
"deviceId"         : "24 BYTES OF FULL ID"  vzdy to musi byt string
"device_count"     : "INDEX OF DEVICE"
}
```



**Reply:**



```
{
"mid"            : "SOME ID",
"status"         : "ok/error",
"error"          : "SOME ERROR MESSAGE", // pouze pokud je status == error
"error_code"     :  SOME NUMBER,         // pouze pokud je status == error
"full_id"        : "SOME FULL ID",       // pouze pokud je status == ok
"short_id"       : "SOME SHORT ID",      // pouze pokud je status == ok
"saved"          :  true/false,          // pouze pokud je status == ok
"interface"      :  SOME NUMBER,         // pouze pokud je status == ok (Viz typedef enum)
"state"          :  SOME NUMBER          // pouze pokud je status == ok
}
```



#### Subtopic "system" 

Systémové příkazy. Viz níže.

#### Subtopic "restart" 

Přistupuje se do něj takto

''XXXXXXXXXXXXXXXXXXXXXXXX/command\_in/system/restart''

Slouží k restartování yody.

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
"status"         : "ok/error",
"error"          : "SOME ERROR MESSAGE", // pouze pokud je status == error
"error_code"     :  SOME NUMBER          // pouze pokud je status == error
}
```

#### Subtopic "ping" 

Přistupuje se do něj takto

''XXXXXXXXXXXXXXXXXXXXXXXX/command\_in/system/ping''

Slouží k pingnutí yody, otestování komunikace, atd...

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
"status"         : "ok/error",
"error"          : "SOME ERROR MESSAGE", // pouze pokud je status == error
"error_code"     :  SOME NUMBER          // pouze pokud je status == error
}
```

#### Subtopic "blink" 

Přistupuje se do něj takto

''XXXXXXXXXXXXXXXXXXXXXXXX/command\_in/system/blink''

Podobně jako ping slouží k otestování komunikace, ale při zaslání příkazu Blink problikne na IODovi RGB dioda.

Pokud má člověk na stole např. 10 IODů a potřebuje si je nějak identifikovat, tohle se hodí.

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
"status"         : "ok/error",
"error"          : "SOME ERROR MESSAGE", // pouze pokud je status == error
"error_code"     :  SOME NUMBER          // pouze pokud je status == error
}
```

#### Chybové stavy 

Každý příkaz může selhat s určitým chybovým kódem. Seznam takovýchto chybových kódů je v \[\[errorcodes:errorcodes\|přehledu chybových kódů\]\].

