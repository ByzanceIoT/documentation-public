# Autobackup

Autobackup je funkce, která se stará o automatickou zálohu aktuálního funkčního kódu na mikrokontroléru pro případ selhání.

## Vlastnosti autobackup

Pokud je autobackup **zapnutý**, aktuálně běžící funkční firmware se sám začne zálohovat a při chybě nové binárky se dokáže tato konfigurace obnovit. Tomuto typu zálohy se říká **dynamická záloha**.

Mezi podmínky spuštění automatického zálohování patří

* úspěšné naběhnutí
* úspěšné připojení k serverům
* bezpečnostní běhový čas backuptime \(viz dále\)

Autobackup přináší výhody i nevýhody.

* Výhodou této varianty je, že pokud aktualizace zařízení selže, vždy se obnoví poměrně poslední funkční konfigurace.
* Nevýhodou je, že zálohovací proces spotřebovává procesorový výkon, a pouští se automaticky na základě výše popsaných podmínek, což může  negativně ovlivnit výkon probíhajícího kódu. Tato varianta není vhodná pro aplikace, které vyžadují kritické časování.

V případě, že je autobackup **vypnutý**, zařízení spoléhá na to, že v záložním sektoru existuje platná **statická záloha,** která byla do zařízení při vypnutí autobackupu doručena. Pokud update binárky neproběhne v pořádku, statická záloha se automaticky obnoví.

* Výhodou je, že stačí zálohu nahrát jednou a zařízení si ji "navždy" pamatuje \(případně do doby než je autobackup zapnutý, čímž se záloha se automaticky přepíše na dynamickou\). Při běhu uživatelského firmware se tak nepouští žádný automatický proces.
* Nevýhoda je to, že pokud update selže, může se obnovit velmi stará fukční konfigurace, která v aktuálním kontextu nemusí být dávno platná.

TO DO 

## Nastavování a zjišťování hodnot

Pokud je nutné režim autobackup změnit, existuje několik možností, jak toho docílit.

* Jediná správná možnost je přepnout režim z Tyriona/Becki. Ostatní režimy můžou být v libovolnou dobu, popř. při restartu "přebity" dle libovůle Tyriona, jehož konfigurace se upřednostňuje v případě konfliktů. Při nahrátí statické zálohy z Tyriona/Becki se automaticky autobackup vypíná nezávisle na okolnostech.
* Další možnost je přepnutí autobackup=1/0 v command režimu bootloaderu a nastavení příkazem backuptime=XXX na určitý počet sekund.



