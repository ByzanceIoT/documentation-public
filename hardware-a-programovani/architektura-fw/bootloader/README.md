# Bootloader

Bootloader je firmwarová komponenta nahraná v každém zařízení Byzance. Automaticky se spouští ihned po zapnutí napájení. Nejčastější úkol bootloaderu je pouze zajištění skoku do hlavního programu,  bootloader však může vykonávat různé další funkce na základě módu, ve kterém se nachází. To může být například aktualizace hlavního programu zařízení, obnovení v případě nefunkčního hlavního firmware a nastavení některých konfiguračních dat.

Jednotlivé režimy jsou popsány v kapitolách [režimy bootloaderu](rezimy-bootloaderu.md), přičemž nejrozsáhlejší část - [command mode](command-mod.md) - má vyhrazenou vlastní kapitolu.

![](../../../.gitbook/assets/bootloader_jump.jpg)

