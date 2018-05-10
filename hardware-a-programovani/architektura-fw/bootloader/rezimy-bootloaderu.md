# Režimy bootloaderu

## Mód JUMP

Pokud není speciálně nastaven jiný mód, bootloader se sám přepne do módu JUMP. Ten sestává z několika kroků:

* Kontrola přitomnosti hlavní aplikace. Pokud hlavní aplikace není dostupná, dojde k přepnutí do command reřimu.
* Spuštění watchdogu \(pokud je nastaveno\) a případné nastavení na příslušnou hodnotu. Blíže vysvětleno v sekci [watchdog](https://github.com/byzance/public-documentation/tree/38b460c46404c197299c0f0a84e3402a9b74c8d7/byzance_documentation/architektura-fw/bootloader/link%20na%20watchdog/README.md).
* **Skok do hlavní aplikace**

## Mód FLASH

Do módu FLASH bootloader automaticky přechází, pokud je zapnutý ''flashflag'' \(více viz [aktualizace firmware](https://github.com/byzance/public-documentation/tree/38b460c46404c197299c0f0a84e3402a9b74c8d7/byzance_documentation/architektura-fw/bootloader/odkaz%20aktualizace%20firmware/README.md)\). V takovém případě potom následují tyto kroky:

* Načtení struktury s informacemi o novém firmware
* Validace a případná oprava velikosti, je-li to možné
* Vymazání interní paměti
* Překopírování všech částí binárky z externí paměti do mikrokontroléru
* Aktualizace informací o novém firmware v mikrokontroléru

Pokud všechny tyto kroky proběhnou v pořádku, následuje

* Vypnutí ''flashflag''
* Zapnutí ''launched'', který slouží ke kontrole funkčnosti nového firmware. Nový firmware tento flag opětovně vypne a tím potvrdí svou funkčnost. Pokud tak nenasatane [watchdog](https://github.com/byzance/public-documentation/tree/38b460c46404c197299c0f0a84e3402a9b74c8d7/byzance_documentation/architektura-fw/bootloader/ODKAZ%20WATCHDOG/README.md)  restartuje mikrokontrolér a spustí poslední funkční verzi firmware pomocí funkce [autobackup](https://github.com/byzance/public-documentation/tree/38b460c46404c197299c0f0a84e3402a9b74c8d7/byzance_documentation/architektura-fw/bootloader/Odkaz%20na%20autobackup/README.md) 
* Vypnutí oprávnění uděleného v proměnné ''trusted'', díky čemuž se firmware označí za potencionálně nefunkční. Firmware bude znovu označený za ověřený poté, co splní příslušná kritéria procesu [autobackup](https://github.com/byzance/public-documentation/tree/38b460c46404c197299c0f0a84e3402a9b74c8d7/byzance_documentation/architektura-fw/bootloader/odkaz%20autobackup/README.md). Poté  co je nový firmware označen flagem "trusted" záložní firmware je přepsan firmwarem aktuálním.

## Mód RESTORE

Tento mód je velmi podobný módu FLASH. Pokud bootloader detekuje zapnutý flag ''launched'' \(tzn. binárka se nedokázala spustit jako hlavní program\), mód je automaticky vyvolán a poslední funkční firmware je obnoven. Flagy ''flashflag'', ''launched'' a ''trusted'' zůstávají nezměněny.

## Mód COMMANDS

Do módu COMMANDS je možné vstoupit několika způsoby

* První spuštění bootloaderu na novém mikrokontroléru
* Kombinací tlačítek \(viz [command režim](https://github.com/byzance/public-documentation/tree/38b460c46404c197299c0f0a84e3402a9b74c8d7/byzance_documentation/architektura-fw/bootloader/odkaz%20na%20bootloader%20comand%20režim/README.md)\)
* Chybí hlavní aplikace
* Bootloader není nakonfigurován \(vypnutá proměnná ''configured'' v [command režimu TO DO](https://github.com/byzance/public-documentation/tree/38b460c46404c197299c0f0a84e3402a9b74c8d7/byzance_documentation/architektura-fw/bootloader/odkaz%20na%20command%20režim/README.md).

## Mód FACTORY RESET

Do módu FACTORY RESET se může dostat bootloader tak, že uživatel stiskne zároveň tlačítka ''restart'' a ''user'', pustí ''restart'' a tlačítko ''user'' drží dlouhou dobu, zpravidla více jak 10 sekund. Mikrokontrolér je nastaven do [defaultních hodnot](https://github.com/byzance/public-documentation/tree/38b460c46404c197299c0f0a84e3402a9b74c8d7/byzance_documentation/architektura-fw/bootloader/odkaz%20na%20defaultní%20hodnoty/README.md) a po této proceduře se přepne do režimu COMMANDS, stejně jako by byl mikrokontrolér poprvé spuštěn.
