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
