## MQTT Topic Commands

Další možné topicy jsou [[Yoda:topic_settings|settings]] a [[Yoda:topic_info|info]]

#### Subtopic "upload"

Příkazy pro část "upload" v procesu [[Yoda:aktualizace_firmware|aktualizace firmware]]. Pomocí následujích 3 příkazů se do Yody dá nahrát binárka k určité komponentě firmware.

#### Subtopic "start" 

Přistupuje se do něj takto
XXXXXXXXXXXXXXXXXXXXXXXX/command_in/upload/start

Polozka "name" obsahuje volitelny textovy popisek (napr. ve zkratce, co dany program dela - je to uzivatelska informace). Maximalni delka je 64B včetně ukončovacího znaku.

Položka "buildId" ma rovněž maximálně 64 znaků.

Položka "version" se sklada ze čtyř části: **jeden** znak (písmeno) a pak tři čísla v rozmezí 0-255. Oddělovačem je **povinně** tečka. Jinými slovy každá ze čtyř části se ukládá do proměnné o velikosti 1B a proto nelze uložit jiné hodnoty. **Neplatné** jsou verze jako "VER0.0.0", "V0.278.0", "AB1580" nebo "V1.01". Sparvne jsou verze "a0.0.0" až "Z255.255.255".

Odpověď na příkaz přijde okamžitě, nicméně to neznamená, že je Yoda připraven binárku přijmout. Je třeba potom kouknout na stav jednotlivých vnitřních komponent, jestli jsou OK.

**Request:**

```
 {
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
XXXXXXXXXXXXXXXXXXXXXXXX/command_in/upload/end

**Request:**

```
{
"mid" : "SOME ID"
}
```

**Reply:**

```
{
"mid" : "SOME ID",
"status" : "ok/error",
"error" : "SOME ERROR MESSAGE", // pouze pokud je status == error
"error_code" : SOME NUMBER // pouze pokud je status == error
}
```

#### Subtopic "data"

Přistupuje se do něj takto
XXXXXXXXXXXXXXXXXXXXXXXX/command_in/upload/data

**Request:**

```
{
"mid" : "SOME ID",
"part" : SOME NUMBER,
"crc" : SOME CRC OF FOLLOWING PART OF DATA BEFORE BASE64,
"size" : 768 BYTES (BEFORE BASE64)
"data" : "BINARY DATA WITH SIZE DEFINED IN LABEL "size",
}
```

**Reply:**

```
{
"mid" : "SOME ID",
"status" : "ok/error",
"error" : "SOME ERROR MESSAGE", // pouze pokud je status == error
"error_code" : SOME NUMBER // pouze pokud je status == error
}
```

#### Subtopic "update"

Jelikož jsme se dohodli že Homer nemusí rozumět tomu jaké zařízení updatuje. Což je důležité do budoucna.
Ale update Yody trvá "hned" update devicu i 3 minuty.... Proto je tu důležitý další parametr. Existují dva různe topicy: topic ''start'' a topic ''status''.

#### Subsubtopic "start"
Přistupuje se do něj takto

XXXXXXXXXXXXXXXXXXXXXXXX/command_in/update/start

Příkazy pro část "update" v procesu [[Yoda:aktualizace_firmware|aktualizace firmware]]. Stručně řečeno, jeho smyslem je odstartovat samotný proces přepisu FLASH paměti aktualizovaného zařízení.

Význam tohoto topicu podle typu zařízení a typu binárky:
* U **Yody**:
* **firmware** - zapsani flagu na update do FLASh paměti, pak čekani na restart od Homera
* **bootloader** - přepis oblasti bootloaderu v interni paměti mikrokontroleru novým bootloaderem, pak čekání na restart
* ** backup** - přepis oblasti s komponentou backup

**Request:**
```
{
"mid" : "SOME ID",
"component" : "firmware/bootloader/backup"
}

```

**Reply:**

```
{
"mid" : "SOME ID",
"status" : "ok/error",
"error" : "SOME ERROR MESSAGE", // pouze pokud je status == error
"error_code" : SOME NUMBER // pouze pokud je status == error
}
```

#### Subtopic "status"
Přistupuje se do něj takto
XXXXXXXXXXXXXXXXXXXXXXXX/command_in/update/status


Topic platný pouze v případě, že jde o ''"update_state" : "longTerm"'' typ nahrávání firmwaru, tj. přenos binárky z Yody na Device, který je časově náročnější. Homer se dotazuje na progress updatu, kde chce znát procentuální stav nahrávání. (Homer se ptá, Yoda odpovídá)



**Request:**

```
{
"mid" : "SOME ID",
"device" : "FULL ID DEVICE, kterého aktuálně Yoda updatuje"
}
```

**Reply:**
```
{
"mid" : "SAME ID",
"status" : "ok/error",
"progress" : 14 <----- int číslo, od 0 do 100 zastupující % update
"error" : "SOME ERROR MESSAGE", // pouze pokud je status == error
"error_code" : SOME NUMBER // pouze pokud je status == error
}
```

#### Subtopic "device"

Subtopic slouží k práci se seznamem zařízení, se kterými bude Yoda komunikovat.
#### Subtopic "add"

Přistupuje se do něj takto
XXXXXXXXXXXXXXXXXXXXXXXX/command_in/device/add

Slouží k přidání nového zařízení do Yody. **Pokud už zařízení už v yodovi existuje, návratový JSON obsahuje status "ok", a result "existing". Pokud zařízení neexistuje, status="ok" a result="new". Result "error" může nastat pouze v případě, že se něco vyloženě pokazí**.

**Request:**

```
{
"mid" : "SOME ID",
"deviceId" : "24 BYTES OF FULL ID"
}
```

**Reply:**

```
{
"mid" : "SOME ID",
"status" : "ok/error",
"error" : "SOME ERROR MESSAGE", // pouze pokud je status == error
"error_code" : SOME NUMBER, // pouze pokud je status == error
"result" : "new/existing" // pouze pokud je status == ok
}
```

#### Subtopic "remove"

Přistupuje se do něj takto
XXXXXXXXXXXXXXXXXXXXXXXX/command_in/device/remove

Slouží k odebrání zařízení z Yody pro potřeby Homera. Reálny vliv je takový, že device **není** ze seznamu zařízení smazán, ale je mu nastaven status ''saved'' na ''false'' a také je jeho ''state'' na ''DISCONNECTED'' (číselně ''0x01'').

**Request:**
```
{
"mid" : "SOME ID",
"deviceId" : "24 BYTES FULL ID" (Index není podporován ze strany homera!! Homer neumí pořadí pole!
}
```

**Reply:**

```
{
"mid" : "SOME ID",
"status" : "ok/error",
"error" : "SOME ERROR MESSAGE", // pouze pokud je status == error
"error_code" : SOME NUMBER, // pouze pokud je status == error
"result" : "removed/missing" // pouze pokud je status == ok
}
```
