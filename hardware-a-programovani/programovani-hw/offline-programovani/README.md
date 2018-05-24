# Offline programování

Každé zařízení Byzance je programovatelné.

{% hint style="info" %}
Mělo by tu být intro o tom, že preferovaný způsob programování je "online"

K tomu ale zatím neexistuje tutoriál.
{% endhint %}

## Programování pomocí ZPP

K programování je možno využít zařízení [Byzance ZPPG3](../../hardware/ostatni/zppg3/). To slouží jako programátor a debugger a propojuje počítač s deskou IODAG3. Díky tomu je paměť IODAG3E připojena jako virtuální mass storage zařízení \(flash disk\) a díky tomu podporuje funkci drag&drop.

{% page-ref page="../../hardware/ostatni/zppg3/" %}

## Programování zařízení DevKit

Zařízení DevKit, má v sobě již zabudovaný programátor a debugger, tudíž není nutné k programování využívat žádné další zařízení jako v případě ZPP. DevKit stačí připojit k PC usb kabelem. V počítači se inicializuje nový flash disk, na který stačí binární kód přetáhnout pomocí drag&drop.

{% page-ref page="../../hardware/ostatni/devkitg3/" %}

## Programování pomocí programátoru ST-link

Vzhledem k tomu, že zařízení IODAG3E má integrovaný procesor STM, je možné ho programovat pomocí programátoru [ST-LINK](http://www.st.com/en/development-tools/st-link-v2.html) a utility [ST-LINK utility](http://www.st.com/en/development-tools/stsw-link004.html).

Utilita má uživatelské GUI, které může být především pro začínající uživatele velkým zjednodušením.

{% page-ref page="upload-kodu-z-gui.md" %}

Pro strojové programování a automatizaci je naopak vhodné programování pomocí konzole. To je shrnuto v příslušném článku.

{% page-ref page="upload-kodu-z-konzole.md" %}

