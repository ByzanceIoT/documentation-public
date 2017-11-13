## MQTT Topic Commands

Další možné topicy jsou \[\[Yoda:topic\_settings\|settings\]\] a \[\[Yoda:topic\_info\|info\]\]

#### Subtopic "upload"

Příkazy pro část "upload" v procesu \[\[Yoda:aktualizace\_firmware\|aktualizace firmware\]\]. Pomocí následujích 3 příkazů se do Yody dá nahrát binárka k určité komponentě firmware.

==== Subtopic "start" ====



Přistupuje se do něj takto

''XXXXXXXXXXXXXXXXXXXXXXXX/command\_in/upload/start''



Polozka ''"name"'' obsahuje volitelny textovy popisek \(napr. ve zkratce, co dany program dela - je to uzivatelska informace\). Maximalni delka je 64B včetně ukončovacího znaku.



Položka ''"buildId"'' ma rovněž maximálně 64 znaků.



Položka ''"version"'' se sklada ze čtyř části: \*\*jeden\*\* znak \(písmeno\) a pak tři čísla v rozmezí 0-255. Oddělovačem je \*\*povinně\*\* tečka. Jinými slovy každá ze čtyř části se ukládá do proměnné o velikosti 1B a proto nelze uložit jiné hodnoty. \*\*Neplatné\*\* jsou verze jako "VER0.0.0", "V0.278.0", "AB1580" nebo "V1.01". Sparvne jsou verze "a0.0.0" až "Z255.255.255".



Odpověď na příkaz přijde okamžitě, nicméně to neznamená, že je Yoda připraven binárku přijmout. Je třeba potom kouknout na stav jednotlivých vnitřních komponent, jestli jsou OK.



\*\*Request:\*\*

