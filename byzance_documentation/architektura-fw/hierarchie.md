#Hierarchie FW

Firmware vyvíjený v prostředí Byzance Code je založen na otevřeném operačním systému Mbed OS. Vývojáři je při programování k dispozici kompletní MBED API, rozšířené o další možnosti v podobě zálohy a obnovení firmware (funkce autobackup), vzdálenou aktualizaci a další užitečné funkce. Tyto další funkce jsou dostupné v rámci Byzance API a uživatelských maker.

Součástí MBED API jsou ARM low level ovladače CMSIS a ovladače HAL výrobce mikrokontroléru. K tomu MBED přidává množství užitečných knihoven na šifrování, konektivitu k internetu a operační systém RTOS. 

![](/assets/architektura_mbed.jpg)

Každý takto vytvořený program, zkompilovaný do binárky je možno distribuovat z cloudového editoru Code jako jednotlivou komponentu ''bootloader'', ''firmware'' nebo ''backup''. Více informací je dostupných v sekci Aktualizace FW. S tímto procesem taktéž úzce souvisí funkce Autobackup pro automatickou zálohu aktuálního funkčního firmware.

![](/assets/aktualizace_hw.jpg)




