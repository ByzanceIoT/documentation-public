# Režimy bootloaderu

## Mód JUMP

Jedná se o výchozí mód, pokud není nastaveno jinak. Cílem je pouze spustit hlavní firmware.

Režim JUMP sestává z několika kroků:

* Kontrola přitomnosti hlavní aplikace. Pokud hlavní aplikace není dostupná, dojde k přepnutí do [command režimu](command-mod.md).
* Spuštění watchdogu \(pokud je nastaveno\) a případné nastavení na příslušnou hodnotu. Blíže vysvětleno v sekci [watchdog](https://github.com/byzance/public-documentation/tree/38b460c46404c197299c0f0a84e3402a9b74c8d7/byzance_documentation/architektura-fw/bootloader/link%20na%20watchdog/README.md).
* **Skok do hlavní aplikace**

## Mód FLASH

Do módu FLASH bootloader automaticky přechází, pokud při předchozím běhu firmware byl přijat nový  validní firmware, který bude nutno nahrát na místo hlavní aplikace \(více viz [aktualizace firmware](https://github.com/byzance/public-documentation/tree/38b460c46404c197299c0f0a84e3402a9b74c8d7/byzance_documentation/architektura-fw/bootloader/odkaz%20aktualizace%20firmware/README.md)\). Mód je detekován tím, že v průběhu běhu předchozího firmware je zapnut signalizátor flashflag, který se po přehrání firmware automaticky vypíná. 

V průběhu aktualizace hlavního programu novým programem probíhají tyto kroky

* Načtení struktury s informacemi o novém firmware
* Validace a případná oprava velikosti, je-li to možné
* Je-li zapnuta funkce [autobackup](../autobackup.md), provede se záloha aktuálně běžícího firmware
* Vymazání interní paměti
* Překopírování všech částí binárky z externí paměti do mikrokontroléru
* Aktualizace informací o novém firmware v mikrokontroléru

Pokud všechny tyto kroky proběhnou v pořádku, následuje

* Vypnutí ''flashflag''
* Zapnutí signalizátoru ''launched'', který slouží ke kontrole funkčnosti nového firmware. Pokud bude po restartu nový firmware nefunkční, "lauchned" se nevypne, [watchdog](https://github.com/byzance/public-documentation/tree/38b460c46404c197299c0f0a84e3402a9b74c8d7/byzance_documentation/architektura-fw/bootloader/ODKAZ%20WATCHDOG/README.md)  restartuje mikrokontrolér a v dalším běhu bootloaderu je aktivován mód RESTORE.

## Mód RESTORE

Tento mód navazuje na mód FLASH.  Pokud se hlavní program po posledním naflashování nespustil \(tedy bootloader detekuje zapnutý flag ''launched'' z režimu FLASH\), mikrokontrolér je po čase resetován [watchdogem](../../funkcionality/watchdog.md), mód RESTORE je automaticky vyvolán a spustí se obnovení posledního funkčního firmwaru, který byl dříve zazálohován funkcí [autobackup](../autobackup.md). 

## Mód COMMANDS

Mód COMMANDS slouží k offline konfiguraci zařízení pomocí [sériové linky.](../../tutorialy/komunikace-po-seriove-lince-uart/) 

Do módu COMMANDS je možné vstoupit několika způsoby

* Kombinací tlačítek
* Chybí hlavní aplikace
* Bootloader není nakonfigurován \(vypnutá proměnná ''configured''\)

Tyto a mnoho dalších informací jsou zpracovány v samostatném článku.

{% page-ref page="command-mod.md" %}

## Mód FACTORY RESET

Mód FACTORY RESET slouží k nastavený [výchozích hodnot](vychozi-hodnoty.md). Je možno jej vyvolat tak, že uživatel stiskne zároveň tlačítka ''restart'' a ''user'', pustí ''restart'' a tlačítko ''user'' drží dlouhou dobu, zpravidla více jak 10 sekund. V této chvíli nastává vymazání paměti a nastavení [výchozích hodnot](vychozi-hodnoty.md), načež se spustí režim COMMANDS, stejně jako by byl mikrokontrolér poprvé spuštěn.

## Výběr režimu

Výběr režimu se řídí pravidly popsanými výše.  Popis doplňuje následující ilustrace stavového automatu mezi jednotlivými režimy.



![](../../../.gitbook/assets/rezimy%20%281%29.png)

