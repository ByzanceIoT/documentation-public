---
description: '#TODO (článek viz ticket HW-1055)'
---

# Upload kódu pomocí ZPP

[ZPPG3](../../hardware/ostatni/daplink.md) je zařízení učené k flashování programu do zařízení IODA jednoduše pomocí drag&drop na virtuální disk, který se vytvoří po připojení do PC.

## Upload hlavního programu

V případě, že máme k dispozici již zkompilovaný kód v binární podobě \(**main.bin**\), připojíme zařízení ZPP do desky a do PC a poté připojíme k desce libovolný zdroj napájení. Po startu desky IODA, dojde i ke startu desky ZPP, který se projeví rychlým problikáním modré LED diody. 

 \#TODO \(Gif připojení ZPP podle ticketu HW-1054\) 

Po zapnutí ZPP, se v PC objeví nový virtuální disk pojmenovaný  **BYZG3\_&lt;pripona&gt;**. Na tento disk pouze drag&drop přetáhneme zkompilovaný binární kód a ZPP automaticky nahraje program do zařízení IODA.

![](../../../.gitbook/assets/git_upload_zpp.gif)

## Upload nové verze Bootloaderu  

Pokud potřebujeme do zařízení nahrát novou verzi [Bootloaderu](../../architektura-fw/bootloader/), postup nahrávání se nepatrně liší. Bootloader se nachází v jiné části paměti zařízení IODA a proto je potřeba před uploadem binárky s novým bootloaderem nejprve potřeba nahrát na ZPP prázdný textový soubor pojmenovaný **BOOTLOAD.txt.** Tím poskytneme ZPP informaci, že jde o bootloader a to automaticky nahraje binární kód do správné části paměti.

![](../../../.gitbook/assets/git_upload_zpp_bootload.gif)

## Chybová hlášení

V případě, že se během uploadu programu vyskytne chyba a ZPP nedokončí program firmware, objeví se na virtuálním disku soubor **FAIL.txt**, ve kterém se vyskytuje chybová hláška. 

![](../../../.gitbook/assets/zpp_fail.png)
