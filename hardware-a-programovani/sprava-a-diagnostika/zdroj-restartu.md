# Zdroj restartu

Zařízení dokáže zjistit zdroj, který způsobil poslední restart. Nízkoúrovňově se jedná o čtení 7 nejvyšších bitů registru  RCC-&gt;CSR mikrokontroléru. Zdrojem může být jedna z následujících 7 událostí:

1. LPWR - vyvoláno low power management komponentou
2. WWDG - vyvoláno window watchdogem \(zaseknutí programu\)
3. IWDG - vyvoláno independent watchdogem \(není použit\)
4. SFT - vyvoláno softwarově \(buď uživatel, nebo vzdáleně\)
5. POR - \(power on reset\) nedostatečné napájecí napětí pro start drží MCU v resetu
6. PIN - resetováno resetovacím pinem
7. BOR - \(brown out reset\) nedostatečné či nestabilní napájecí napětí v průběhu běhu mikrokontoléru způsobí reset. Hranici je možno nastavovat.

Čtení zdroje restartu probíhá pouze při prvním dotazu po startu zařízení. Dotazem je zdroj je smazán z FLASH a překopírován do RAM, kde se drží až do konce běhu zařízení. Pro všechny další dotazy v průběhu běhu zařízení se používá hodnota z RAM. Tento postup zamezuje opotřebení FLASH paměti neustálými přepisy po restartu. Zdroj restartu může obsahovat více položek najednou, pokud mezi jednotlivými dotazy proběhlo několik různých druhů restartu.







