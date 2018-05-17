# Paměti

Jednotka IODAG3E obsahuje několik druhů pamětí, kde každý typ má svůj účel a svá specifika. Jedná se o volatilní paměť RAM a nevolatilní paměť FLASH integrovanou v pouzdře mikrokontroléru a o větší externí FLASH paměť.

* RAM
  * 256 kB SRAM \(včetně 64 kB CCM\)
  * 4 kB zálohované SRAM \(zálohováno _VBAT_ zdrojem\) 
  * součást mikrokontroléru sloužící pro data běžícího firmware
* FLASH
  * 2 MB v mikrokontroléru
  * rozděleno na stránky o různých velikostech
  * slouží pro firmware a bootloader jednotky
* externí FLASH
  * velikost 64 Mb
  * připojena přes SPI rozhraní k mikrokontroléru
  * slouží pro uložení konfigurace, záložního firmware a jako uživatelský prostor



