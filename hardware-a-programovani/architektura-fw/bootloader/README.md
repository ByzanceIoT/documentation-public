# Bootloader

Bootloader \(tzv. zavaděč\) je firmwarová komponenta nahraná v každém zařízení Byzance. Automaticky se spouští ihned po zapnutí napájení. Nejčastější úkol bootloaderu je pouze zajištění skoku do hlavního programu. Bootloader však může vykonávat různé další funkce na základě módu, ve kterém se nachází. Mezi módy může spadat například [aktualizace hlavního programu](rezimy-bootloaderu.md#mod-flash) zařízení, [obnovení v případě nefunkčního hlavního firmware](rezimy-bootloaderu.md#mod-restore) a [nastavení některých konfiguračních dat](rezimy-bootloaderu.md#mod-commands).

Jednotlivé režimy jsou popsány v kapitolách [režimy bootloaderu](rezimy-bootloaderu.md), přičemž nejrozsáhlejší část - [command mode](command-mod.md) - má vyhrazenou vlastní kapitolu.

![](../../../.gitbook/assets/bootloader_jump.jpg)

