# Autobackup

Autobackup je funkce, která se stará o automatickou zálohu zdrojového kódu na mikrokontroléru.

Při update firmwaru je klíčové, aby update proběhl celý hladce a bez chyb, případně při detekci chyby byl update zastaven tak, aby nedošlo k porušení aktuálně běžícího firmwaru. Není možno ale vyloučit poruchu \(např. vytržením zařízení od napájení\), případně nefukční binárku zkompilovanou například pro jiný target.

Pokud se nová binárka z jakéhokoliv důvodu poškodí a nenaběhne, v té chvíli už by nebylo možné zařízení bez použití programátoru "oživit"., čímž by se stalo "bricknuté". Proto je nutné mít záložní binárku, která v takovém případě naběhne a zařízení zachrání i bez použití programátoru. Přesně k tomuto slouží vlastnost autobackup.

## Vlastnosti autobackup

Pokud je autobackup \*\*zapnutý\*\*, aktuálně běžící firmware se sám začne zálohovat a při chybě nové binárky se dokáže tato konfigurace obnovit. Tomuto typu zálohy se říká \*\*dynamická záloha\*\*. Mezi podmínky spuštění automatického zálohování patří úspěšné naběhnutí + úspěšné připojení k serverům + bezpečnostní běhový čas //backuptime//.

* Výhodou této varianty je, že pokud update zařízení selže, vždy se obnoví poměrně nedávná funkční konfigurace.
* Bohužel zálohovací proces spotřebovává procesorový výkon, a pouští se automaticky na základě výše popsaných podmínek, což může  negativně ovlivnit výkon probíhajícího kódu.

V případě, že je autobackup \*\*vypnutý\*\*, zařízení spoléhá na to, že v záložním sektoru existuje platná \*\*statická\*\* záloha, která byla do zařízení při vypnutí autobackupu doručena. Pokud update binárky neproběhne v pořádku, statická záloha se automaticky obnoví.

* Výhodou je, že stačí zálohu nahrát jednou a zařízení si ji "navždy" pamatuje \(případně do doby než je autobackup zapnutý, čímž se záloha se automaticky přepíše na dynamickou\). Při běhu uživatelského firmware se tak nepouští žádný automatický proces.
* Nevýhoda je to, že pokud update selže, může se obnovit velmi stará fukční konfigurace, která v aktuálním kontextu nemusí být dávno platná.

## Proměnná backuptime

Pokud je \*\*autobackup zapnutý\*\*, firmware začne brát v potaz proměnnou \*\*backuptime\*\*. Tato proměnná vyjadřuje ochranný čas od startu programu a následného připojení k serverům Byzance do spuštění procesu automatického backupu \(vyjádřeném v sekundách\).

Nastavená minimální hodnota by měla být alespoň 60 sekund, aby bylo při zálohování aktuálně probíhajícího firmware ověřeno, že firmware dokáže bez pádu daný čas běžet, tudíž je velká pravděpodobnost, že se dokáže během daného času i updatovat. Optimální hodhota je 5 minut a víc.

## Nastavování a zjišťování hodnot

Pokud je nutné režim autobackup změnit, existuje několik možností, jak toho docílit.

\* Jediná správná možnost je přepnout režim z Tyriona/Becki. Ostatní režimy můžou být v libovolnou dobu, popř. při restartu "přebity" dle libovůle Tyriona, jehož konfigurace se upřednostňuje v případě konfliktů. Při nahrátí statické zálohy z Tyriona/Becki se automaticky autobackup vypíná nezávisle na okolnostech.

\* další možnost je přepnutí autobackup=1/0 v command režimu bootloaderu a nastavení příkazem backuptime=XXX na určitý počet sekund.

\* možné je i zjištění/nastavení pomocí příslušeného MQTT příkazu v topicích \[\[Yoda:topic\_settings\|settings\]\] a \[\[Yoda:topic\_info\|info\]\]

