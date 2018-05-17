# Interní paměť mikrokontrolérui

## Práce s interní pamětí

Je-li třeba pracovat s interní pamětí mikrokontroléru, čtení je poměrně triviální. Data lze číst po bytech přímo z konkrétní požadované adresy. Zápis se ale trochu komplikuje. Paměť je rozdělená na jednotlivé stránky, které jsou u Cortex M0 fixní, většinou o velikosti 2KiB, u Cortex M4 architektury se však velikosti výrazně liší.

## Rozdělení sektorů

Většina mikrokontrolérů Cortex M4 má stránky do 1MB velikosti paměti rozdělené takto

* Sektor 0-3   -&gt; 16 KB
* Sektor 4     -&gt; 64 kB
* Sektor 5-11  -&gt; 128 kB

Pokud je paměť složena z více paměťových bank \(např. interní flash 2MiB je nejčastěji 2x1MiB\), pattern rozdělení sektorů u druhého MB se opakuje

* Sektor 12-15 -&gt; 16 KB
* Sektor 16    -&gt; 64 kB
* Sektor 17-23 -&gt; 128 kB

Uživatelská práce s interní pamětí se nedoporučuje, protože může dojít k poškození firmware nebo bootloaderu. Výše uvedené skutečnosti je třeba reflektovat \(především při mazání, kde se může stát, že je třeba smazat jenom několik bytů dat, ale technologie FLASH smaže celou stránku společně i s jinými daty\).

## Rozsahy adres

### IODAG3E

* Velikost celkem 2 MiB \(0x00200000\) - celkem 24 sektorů
* Z toho bootloader 64 KiB \(0x00010000\) - sektory 0 - 3
* Z toho firmware 1984 KiB \(0x001F0000\) - sektory 4 - 23

```text
     ============
    | 0x08000000 |
    |    ...     | (Bootloader, 64 KiB in total)
    | 0x0800FFFF |
    |============|
    | 0x08010000 |
    |    ...     | (Size depending on target)
    |    end     |
     ============
```

Adresy 0x08000000 a 0x08010000 je tedy třeba znát při ručním nahrávání bootloaderu nebo firmware.

