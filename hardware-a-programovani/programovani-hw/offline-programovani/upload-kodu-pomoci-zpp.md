# Upload kódu Drag&drop

Upload kódu pomocí drag and drop je operace, kdy se zařízení připojí jako virtuální [mass storage zařízení](https://en.wikipedia.org/wiki/Mass_storage) \(flash disk\) a poté umožňuje pouhým přetažení souboru s firmware aktualizovat kód zařízení. 

Funkcionalita drag&drop je podmíněna přítomností programátoru a debuggeru, založeného na technologii [DAPlink](https://github.com/ARMmbed/DAPLink). DAPlink může být připojen buď externě jako v případě desky [ZPP](../../hardware/ostatni/zppg3/), či může být součástí zařízení, například [DKG3](../../hardware/ostatni/devkitg3/).

## Upload hlavního programu

V případě, že je k dispozici již zkompilovaný kód v binární podobě \(**main.bin**\), připojí se zařízení s DAPlink  do PC a poté se zajistí napájení. Správnou inicializaci by měl DAPlink signalizovat krátkým zablikáním.

 \#TODO \(Gif připojení ZPP podle ticketu HW-1054\) 

Po inicializaci se v PC objeví nový virtuální disk pojmenovaný  **BYZG3\_&lt;pripona&gt;**. Na tento disk stačí pouze pomocí drag&drop přetáhnout zkompilovaný binární kód a DAPlink automaticky nahraje program do zařízení.

![](../../../.gitbook/assets/git_upload_zpp.gif)

## Upload nové verze Bootloaderu  

Pokud je třeba do zařízení nahrát novou verzi [bootloaderu](../../architektura-fw/bootloader/), postup nahrávání se nepatrně liší. Bootloader se nachází v jiné části paměti zařízení. Proto je potřeba před uploadem binárky s novým bootloaderem nejprve potřeba nahrát pomocí drag&drop prázdný textový soubor pojmenovaný **BOOTLOAD.txt.** Tím se DAPlink přeprogramuje na programování bootloaderu, díky čemuž je automaticky nahrán binární kód do správné části paměti. Po dokončení operace proběhne restart programovaného zařízení a DAPlink se sám přepne zpět do módu programování firmware.

![](../../../.gitbook/assets/git_upload_zpp_bootload.gif)

## Chybová hlášení

V případě, že se během uploadu programu vyskytne chyba a programování není dokončeno, objeví se na virtuálním disku soubor **FAIL.txt**, ve kterém se vyskytuje chybová hláška. 

![](../../../.gitbook/assets/zpp_fail.png)

Programátor je dále možné ovládat pomocí MSD příkazů. Jejich zadávání spočívá v tom, že jsou na flashdisk nahrávány soubory s různými názvy. Ve výchozím nastavení jsou příkazy prováděny pouze pokud je současně stisknuto tlačítko ISP/RST \(mód automation je vypnutý\). Podrobnosti viz.: [MSD Commands](https://github.com/mbedmicro/DAPLink/blob/master/docs/MSD_COMMANDS.md).

