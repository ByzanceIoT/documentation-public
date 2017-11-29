## MQTT Topic Commands

Další možné topicy jsou \[\[Yoda:topic\_settings\|settings\]\] a \[\[Yoda:topic\_info\|info\]\]

#### Subtopic "upload"

Příkazy pro část "upload" v procesu \[\[Yoda:aktualizace\_firmware\|aktualizace firmware\]\]. Pomocí následujích 3 příkazů se do Yody dá nahrát binárka k určité komponentě firmware.

#### Subtopic "start"

Přistupuje se do něj takto

''XXXXXXXXXXXXXXXXXXXXXXXX/command\_in/upload/start''

Položka ''"usr\_name"'' obsahuje volitelny textovy popisek \(napr. ve zkratce, co dany program dela - je to uzivatelska informace\). Maximalni delka je 64B včetně ukončovacího znaku.

Položka ''"build\_id"'' ma rovněž maximálně 31 znaků.

Položka ''"version"'' se skladá: "v1.2.3-alpha","v1.2.3-beta" nebo "v1.2.3"

Odpověď na příkaz přijde okamžitě, nicméně to neznamená, že je Yoda připraven binárku přijmout. Je třeba potom kouknout na stav jednotlivých vnitřních komponent, jestli jsou OK.

**Request:**

```
"mid"            : "SOME ID",
"size"           :  SIZE OF WHOLE BINARY FILE BEFORE BASE64,
"crc"            :  CHECKSUM OF WHOLE BINARY FILE BEFORE BASE64,
"build_id"        : "SOME BUILD_ID - UUID 36 Chars", (No space allowed) (31 char max)
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

