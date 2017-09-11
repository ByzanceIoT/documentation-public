# CPU load



Interní implementace využívá RTOS vlastnosti ''idle\_hook''. Scheduler operačního systému automaticky volá a obsluhuje jednotlivá vlákna a vnitřní komponenty a pokud není co k obsluze, periodicky se začne volat funkce připojená pomocí metody ''attach\_idle\_hook''. Byzance třída obsahuje počítadlo, kolikrát za sekundu se callback ''idle\_hook'' zavolal a toto počítadlo vždy na konci dané periody vynuluje. Z počtu zavolání ''idle\_hook'' se uvnitř Byzance třídy počítá využití mikrokontroléru. Počet zavolání ''idle\_hook'' závisí na typu použitého mikrokontroléru a frekvenci, na které běží. Další informace je možné nalézt v nejnovější \[\[https://docs.mbed.com/docs/mbed-os-api-reference/en/latest/APIs/tasks/rtos/\|API MBED\]\].



## Jak lze zjistit využití mikrokontroléru

  \* Dotazem do \[\[yoda:topic\_info\#informace\_o\_cpuload\|info topicu\]\]

  \* Ve \[\[tutorial:webview\| webovém rozhraní\]\]


