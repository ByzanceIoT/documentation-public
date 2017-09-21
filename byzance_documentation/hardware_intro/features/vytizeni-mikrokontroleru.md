# CPU load

Vytížení mikrokontroléru detekuje proměnná CPU load. Vyjadřuje vytížení mikrokontroléru \(operačního systému\) v procentech. Nevytížený mikrokontrolér má ''cpuload'' rovný 0%, naopak například napsání ''while\(true\);'' či složitý výpočet vytíží procesor na 100%.

Interní implementace využívá RTOS vlastnosti ''idle\_hook''. Scheduler operačního systému automaticky volá a obsluhuje jednotlivá vlákna a vnitřní komponenty a pokud není co k obsluze, periodicky se začne volat funkce připojená pomocí metody ''attach\_idle\_hook''. Byzance třída obsahuje počítadlo, kolikrát za sekundu se callback ''idle\_hook'' zavolal a toto počítadlo vždy na konci dané periody vynuluje. Z počtu zavolání ''idle\_hook'' se uvnitř Byzance třídy počítá využití mikrokontroléru. Počet zavolání ''idle\_hook'' závisí na typu použitého mikrokontroléru a frekvenci, na které běží. Další informace je možné nalézt v nejnovější \[\[[https://docs.mbed.com/docs/mbed-os-api-reference/en/latest/APIs/tasks/rtos/\|API](https://docs.mbed.com/docs/mbed-os-api-reference/en/latest/APIs/tasks/rtos/|API) MBED\]\].

Je nutné dbát na to, že číslo je pouze orientační a nevyjadřuje využití jednotlivých periferií, ale samotného ARM jádra.

## Jak lze zjistit využití mikrokontroléru

* Ve webovém rozhraní
* Pomocí Byzance API



