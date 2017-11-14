# Identifikace zařízení

Všechny zařízení IODA mají ve FLASH paměti svého mikrokontroléru STM32 z výroby naprogramovaný **jedinečný identifikátor čipu**. Jedná se o 96 bitů dlouhé číslo reprezentované **24 hexadecimálními ASCII znaky**. Vyskytuje se na specifické adrese v paměti (liší se podle rodiny mikrokontroléru) a lze ho pouze číst. Toto číslo je Byzance interně označováno jako [Full ID](identifikace-zarizeni/full-id.md)

