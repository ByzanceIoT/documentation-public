# Autobackup

Autobackup je funkce, která se stará o automatickou zálohu aktuálního funkčního kódu na mikrokontroléru pro případ selhání.

## Vlastnosti autobackup

Pokud je funkce autobackup **zapnutá**, při nahrávání nového firmware se původně běžící firmware zazálohuje a při chybě nové binárky se dokáže tato konfigurace obnovit. Tomuto typu zálohy se říká [**dynamická záloha**](autobackup.md#dynamicka-zaloha).

V případě, že je automatická záloha posledního funkčního firmware nežádoucí a je třeba jeden záložní firmware pro všechny situace, funkce autobackup je **vypnutá** a tomuto typu se říká [**statická záloha**](autobackup.md#staticka-zaloha).

![](../../../.gitbook/assets/autobackup.png)

## Dynamická záloha

Zapnutý autobackup, tedy dynamická záloha přináší určité výhody i nevýhody.

* Výhodou této varianty je, že pokud aktualizace zařízení selže, vždy se obnoví poslední funkční konfigurace.
* Nevýhodou je, že při každé aktualizaci na novou verzi firmware musí proběhnout ještě záloha původního firmware. Toto může trvat nějaký čas. Řádově se jedná zhruba o 20 sekund navíc při každé aktualizaci.

## Statická záloha

V případě, že je autobackup **vypnutý**, zařízení spoléhá na to, že v záložním sektoru existuje platná **statická záloha,** která byla do zařízení před vypnutím autobackupu doručena. Pokud aktualizace binárky neproběhne v pořádku, statická záloha se automaticky obnoví.

* Výhodou je, že stačí zálohu nahrát jednou a zařízení si ji "navždy" pamatuje \(případně do doby než je autobackup zapnutý, čímž se záloha se automaticky přepíše na dynamickou\).
* Nevýhoda je to, že pokud update selže, může se obnovit velmi stará fukční konfigurace, která v aktuálním kontextu nemusí být dávno platná.

## Nepovolené stavy

Pro zachování bezpečnosti existují nepovolené stavy, které zařízení nedopustí.

| autobackup | backup | změna AB | změna B | změna FW |
| :--- | :--- | :--- | :--- | :--- |
| 1 | 0 | 1 | 1 | **0** |
| 0 | 1 | 1 | 1 | 1 |
| 1 | 0 | **0** | 1 | 1 |
| 1 | 1 | 1 | 1 | 1 |

blabla

1. Pokud je vypnutý autobackup a neexistuje validní backup, není možno nahrávat firmware. V případě nahrání chybného firmware by bylo zařízení poškozeno a nedokázalo by se samo obnovit. Řešením je před nahráním firmware buď zapnout autobackup, nebo nahrát validní backup.
2. Pokud neexistuje validní backup, nelze vypnout autobackup. Řešením je nahrátí nového firmware, čímž se validní backup vytvoří ze současného firmware, případně nahrátí validního backupu.

## Nastavování a zjišťování hodnot

Pokud je nutné režim autobackup změnit, existuje několik možností, jak toho docílit. Podrobnější popis je v kapitole konfigurace, přičemž doporučováno je měnit nastavení pomocí nástroje v Portalu Byzance.

{% page-ref page="../../sprava-a-diagnostika/konfigurace-zarizeni/" %}

