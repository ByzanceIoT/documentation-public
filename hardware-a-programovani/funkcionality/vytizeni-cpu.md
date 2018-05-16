# Vytížení zařízení

Vytížení mikrokontroléru detekuje proměnná CPU load. Vyjadřuje se v procentech 0 - 100. Nevytížený mikrokontrolér má ''cpuload'' rovný 0%, naopak například napsání ''while\(true\);'' či složitý výpočet vytíží procesor na 100%.

**Je nutné dbát na to, že číslo je pouze orientační a nevyjadřuje využití jednotlivých periferií, ale samotného schreduleru RTOS.**

Interní implementace využívá RTOS vlastnosti ''idle\_hook''. Scheduler operačního systému automaticky volá a obsluhuje jednotlivá vlákna a vnitřní komponenty a pokud není co k obsluze, periodicky se začne volat funkce připojená pomocí metody ''attach\_idle\_hook''. Byzance třída obsahuje počítadlo, kolikrát za sekundu se callback ''idle\_hook'' zavolal a toto počítadlo vždy na konci dané periody vynuluje. Z počtu zavolání ''idle\_hook'' se uvnitř Byzance třídy počítá "vytížení zařízení". Počet zavolání ''idle\_hook'' závisí na typu použitého mikrokontroléru a frekvenci, na které běží. 

## Jak lze zjistit využití mikrokontroléru

* Ve webovém rozhraní
* Pomocí Byzance API

