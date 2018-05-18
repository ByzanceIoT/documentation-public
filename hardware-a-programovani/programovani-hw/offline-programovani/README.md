# Offline programování

Každé zařízení Byzance je programovatelné. 

{% hint style="info" %}
Mělo by tu být intro o tom, že preferovaný způsob programování je "online"

K tomu ale zatím neexistuje tutoriál.
{% endhint %}

## Programování pomocí ZPP

K programování je možno využít zařízení [Byzance ZPPG3](../../hardware/ostatni/zppg3/), které umožňuje drag&drop programování. Toto zařízení připojíme k programovacímu konektoru a PC a zařízení IODA zapojíme do napájení.  V počítači se hned poté inicializuje nový flash disk, na který stačí binární kód vložit a automaticky se nahraje do zařízení.

 \#TODO \(GIF pripojení ZPP do počítače a IODY - ticket  [HW-1054](https://youtrack.byzance.cz/youtrack/issue/HW-1054)\)

Podrobný návod programování pomocí ZPP lze nalézt v sekci [Upload kódu pomocí ZPP](upload-kodu-pomoci-zpp.md). 

### Programování zařízení DevKit

Zařízení DevKit, má v sobě programátor zabudovaný, tudíž není nutné k programování využívat žádné další zařízení. DevKit stačí připojit k PC usb kabelem a v počítači se inicializuje nový flash disk, na který stačí binární kód přetáhnout drag&drop stejně jako pomocí ZPP.

### Programování pomocí programátoru ST-link

Vzhledem k tomu, že zařízení IODAG3E  má integrovaný procesor STM, je možné ho programovat pomocí programátoru ST-link. Pro více informací pokračujte do sekce [Upload kódu z GUI](upload-kodu-z-gui.md). 

