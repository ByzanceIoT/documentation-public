# Rozložení a využití paměti

## RAM

Pro správné pochopení je vhodné nejdříve přečíst si obecný článek o nevolatilní paměti. Níže uvedený přehled obecné informace doplňuje a zpřesňuje pro konkrétní target IODAG3E.

Celkově je k dispozici

* RAM 128 kB
* CCM 64 kB

Orientační výčet paměti pro minimální projekt

* .data 1500 B
* .bss 48 kB
* stack 26 kB
* oblast heap není známa \(přibližně 48 kB\)

Tabulka oblastí je v následující tabulce

| oblast | .bss | .data | heap | stack |
| :--- | :--- | :--- | :--- | :--- |
| umístění | CCM | CCM | RAM | RAM |
| velikost | 1500 B | 48 kB | 48 kB | 26 kB |

![](/assets/ram_ccm.png)

Jak je patrné, oblasti .bss a .data \(veškeré globální a statické proměnné\) jsou v CCM. Nevýhodou tohoto řešení je fakt, že k těmto datům nemůže přistupovat DMA. Problém lze řešit tak, že data pro DMA budou dynamicky alokována v oblasti v heap.

## Externí paměť

* 8MB \(64Mb\) externí flash paměť \(\[\[tutorial:nonvolatile\| dokumentace\]\]\) 


