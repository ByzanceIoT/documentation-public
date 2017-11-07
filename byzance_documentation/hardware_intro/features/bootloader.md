## Bootloader

FIXME jak ho vyvolat?!

Vstup do bootloaderu je vizuálně signalizován [Led modulem TO DO odkaz na ledmodul](odkaz na ledmodul).

Každé zařízení má v sobě nahraných více do jisté míry nezávislých programů. Typicky jde o tyto:
  * bootloader,
  * hlavní program,
  * záložní program,
  * programový buffer.

Každý program má ve FLASH paměti vyhrazeno pevné místo, tj. má [danou počáteční adresu a max. velikost - TO DO odkaz](ODKAZ na adresaci).

#### Činnost bootloaderu 

Po zapnutí napájení zařízení vždy začne vykonávat instrukce z bootloaderu. Úkolem bootloaderu je zajistit aktualizaci hlavního programu zařízení, obnovení v případě nefunkčního hlavního firmware a nastavení některých konfiguračních dat.

#### Mód JUMP 
Pokud není nastaven jiný mód, bootloader se sám přepne do módu JUMP. Ten sestává z několika kroků:
  * Kontrola, jestli je přítomna hlavní aplikace - pokud není, dojde k přepnutí do command_mode.
  * Zapnutí watchdogu (pokud má být zapnut) a případné nastavení na příslušnou hodnotu. Více v sekci [watchdog](link na watchdog).
  * **Skok do hlavní aplikace**


#### Mód FLASH 
Do módu FLASH bootloader automaticky přechází, pokud je zapnutý ''flashflag'' (více viz [aktualizace firmware TO DO](odkaz aktualizace firmware)). V takovém případě potom následují tyto kroky:

  * načtení struktury s informacemi o novém firmware,
  * validace a případná oprava velikosti, je-li to možné a smyslné,
  * vymazání interní paměti
  * překopírování všech částí binárky z externí paměti do mikrokontroléru
  * aktualizace informací v příslušné struktuře o novém firmware v mikrokontroléru

Pokud všechny tyto kroky proběhnou v pořádku, následuje
  * vypnutí ''flashflag''
  * zapnutí ''launched'', který by se měl v naběhnutém firmware vypnout a pokud tak nenastane (binárka je vadná), [[feature:watchdog| watchdog]]  restartuje mikrokontrolér a spustí obnovu poslední funkční binárky vyrobené pomocí procesem [[feature:autobackup|autobackup]] 
  * vypnutí oprávnění udělené do proměnné ''trusted'', díky čemuž se firmware označí za potencionálně nefunkční. Oprávnění se zvýší až pokud běžící firmware splní příslušná kritéria procesu [[feature:autobackup| autobackup]], kdy se automaticky může spustit záloha.

#### Mód RESTORE 
Tento mód je velmi podobný módu FLASH. Pokud bootloader detekuje zapnutý flag ''launched'' (tzn. binárka se nedokázala spustit jako hlavní program), mód je automaticky vyvolán a poslední funkční firmware je obnoven. Flagy ''flashflag'', ''launched'' a ''trusted'' zůstávají nezměněny.

#### Mód COMMANDS 

Do módu COMMANDS je možné vstoupit několika způsoby
  * první spuštění bootloaderu na novém mikrokontroléru
  * kombinací tlačítek (viz [bootloader command režim TO DO ](odkaz na bootloader comand režim))
  * chybějící hlavní aplikace
  * bootloader není nakonfigurován (vypnutá proměnná ''configured'' v [command režimu TO DO](odkaz na command režim).

#### Mód WIFIAP 

FIXME Nyní nepoužito

==== Mód FACTORY RESET ====

Do módu FACTORY RESET se může dostat bootloader tak, že uživatel stiskne zároveň tlačítka ''restart'' a ''user'', pustí ''restart'' a tlačítko ''user'' drží dlouhou dobu, zpravidla více jak 10 sekund. Mikrokontrolér je nastaven do [[Bootloader:defaults| defaultních hodnot]] a po této proceduře se přepne do režimu COMMANDS, stejně jako by byl mikrokontrolér poprvé spuštěn.
===== Proces aktualizace hlavního programu v Device =====  

FIXME aktuálně nevyužito a do budoucna device asi dostanou extmem a budou normálně pracovat s bufferem, je to bezpečnější a systematičtější

Terminologie:

  * **aktuální** program je ten, který naposledy běžel z interní paměti Yody
  * **nový** program je ten, který v Yodovi zatím neběžel

  - Bootolader provede načtení parametrů **nového** programu z konfig. paměti a provedene validaci.
  - Funkce autobackup je u device vždy zapnutá a nedá se vypnout.
  - Homer dříve [[Yoda:upload| nahrál do device]] do části nového programu **nový** program. 
  - Bootloader prohodí **aktuální** program s **novým** programem. Tím se z **nového** programu stane **aktuální**
  - Zapíše se informace o **aktuálním** programu v Yodovi do konfigurační paměti.
  - Na závěr bootloader skočí na začátek **aktuálního** programu a začne ho vykonávat.

===== Aktualizace firmware =====  

Aktualizace firmware je zdokumentována na stránce [[Yoda:upload| Aktualizace firmware]].
Sestává ze 2 sad kroků
  * **upload**, kdy se binárka přenese z Homera do Yody a uloží se do jeho externí paměti.
  * **update**, kdy je yodovi specifikováno, co s danou binárkou má provést (aktualizuje svůj firmware, nebo několik zařízení atd..)

===== Vývojový diagram =====

FIXME Zde bude obrázkový vývojový diagram co a jak
