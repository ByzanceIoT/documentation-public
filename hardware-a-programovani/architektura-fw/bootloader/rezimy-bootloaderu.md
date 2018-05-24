# Režimy bootloaderu

Bootloader \(tzv. zavaděč\) je softwarová komponenta, která se spouští jako první při zapnutí zařízení. Jejím úkolem je většinou pouze skok do hlavního programu. Má ale i několik dalších módů, které popisuje tato kapitola. Speciálním režimem je [mód commands](command-mod.md), díky němuž je možno [konfigurovat zařízení](../../sprava-a-diagnostika/konfigurace-zarizeni.md).

## Mód JUMP

Jedná se o výchozí mód, pokud není nastaveno jinak. Cílem je pouze spustit hlavní firmware.

Režim JUMP sestává z několika kroků:

* Kontrola přitomnosti hlavní aplikace. Pokud hlavní aplikace není dostupná, dojde k přepnutí do [command režimu](command-mod.md).
* Spuštění watchdogu \(pokud je nastaveno\) a případné nastavení na příslušnou hodnotu. Blíže vysvětleno v sekci [watchdog](../../funkcionality/watchdog.md).
* **Skok do hlavní aplikace**

## Mód FLASH

Do módu FLASH bootloader automaticky přechází, pokud při předchozím běhu firmware byl přijat nový validní firmware, který bude nutno nahrát na místo hlavní aplikace \(více viz [aktualizace firmware](../aktualizace-fw.md)\). Mód je detekován tím, že v průběhu běhu předchozího firmware je zapnut signalizátor flashflag, který se po přehrání firmware automaticky vypíná.

V průběhu aktualizace hlavního programu novým programem probíhají tyto kroky

* Načtení struktury s informacemi o novém firmware
* Validace a případná oprava velikosti, je-li to možné
* Je-li zapnuta funkce [autobackup](../autobackup.md), provede se záloha aktuálně běžícího firmware
* Vymazání interní paměti
* Překopírování všech částí binárky z externí paměti do mikrokontroléru
* Aktualizace informací o novém firmware v mikrokontroléru

Pokud všechny tyto kroky proběhnou v pořádku, následuje

* Vypnutí ''flashflag''
* Zapnutí signalizátoru ''launched'', který slouží ke kontrole funkčnosti nového firmware. Pokud bude po restartu nový firmware nefunkční, "lauchned" se nevypne, [watchdog](../../funkcionality/watchdog.md) restartuje mikrokontrolér a v dalším běhu bootloaderu je aktivován mód RESTORE.

## Mód RESTORE

Tento mód navazuje na mód FLASH. Pokud se hlavní program po posledním naflashování nespustil \(tedy bootloader detekuje zapnutý flag ''launched'' z režimu FLASH\), mikrokontrolér je po čase resetován [watchdogem](../../funkcionality/watchdog.md), mód RESTORE je automaticky vyvolán a spustí se obnovení posledního funkčního firmwaru, který byl dříve zazálohován funkcí [autobackup](../autobackup.md).

## Mód COMMANDS

Mód COMMANDS slouží k offline konfiguraci zařízení pomocí [sériové linky.](../../tutorialy/komunikace-po-seriove-lince-uart-s-pc/)

Do módu COMMANDS je možné vstoupit několika způsoby

* Kombinací tlačítek
* Chybí hlavní aplikace
* Bootloader není nakonfigurován \(vypnutá proměnná ''configured''\)

Tyto a mnoho dalších informací jsou zpracovány v samostatném článku.

{% page-ref page="command-mod.md" %}

## Mód FACTORY RESET

Mód FACTORY RESET slouží k nastavený [výchozích hodnot](vychozi-hodnoty.md). Je možno jej vyvolat tak, že uživatel stiskne zároveň tlačítka ''restart'' a ''user'', pustí ''restart'' a tlačítko ''user'' drží dlouhou dobu, zpravidla více jak 10 sekund. V této chvíli nastává vymazání paměti a nastavení [výchozích hodnot](vychozi-hodnoty.md), načež se spustí režim COMMANDS, stejně jako by byl mikrokontrolér poprvé spuštěn.

## Výběr režimu

Výběr režimu se řídí pravidly popsanými výše. Ucelený přehled a přechody mezi jednotlivými režimy shrnuje následující ilustrace stavového automatu bootloaderu.

![](../../../.gitbook/assets/rezimy%20%281%29.png)

