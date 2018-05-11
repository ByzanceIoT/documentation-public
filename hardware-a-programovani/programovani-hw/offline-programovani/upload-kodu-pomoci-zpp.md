---
description: '#TODO (článek viz ticket HW-1055)'
---

# Upload kódu pomocí ZPP

[ZPPG3](../../hardware/ostatni/daplink.md) je zařízení učené k flashování programu do zařízení IODA jednoduše pomocí drag&drop na virtuální disk, který se vytvoří po připojení do PC.

## Upload hlavního programu

V případě, že máme k dispozici již zkompilovaný kód v binární podobě \(**main.bin**\), připojíme zařízení ZPP do desky a do PC a poté připojíme k desce libovolný zdroj napájení. Po startu desky IODA, dojde i ke startu desky ZPP, který se projeví rychlým problikáním modré LED diody. 

 \#TODO \(Gif připojení ZPP podle ticketu HW-1054\) 

Po zapnutí ZPP, se v PC objeví nový virtuální disk pojmenovaný  **BYZG3\_&lt;pripona&gt;** 

![](../../../.gitbook/assets/git_upload_zpp.gif)

