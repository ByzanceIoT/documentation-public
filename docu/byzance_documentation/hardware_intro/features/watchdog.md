# Watchdog

Watchdog je vlastnost mikrokontroléru, která se zapíná a konfiguruje v bootloaderu před startem uživatelského programu.

Pokud je watchdog zapnutý a nastavený na určitý čas, musí se pravidelně softwarově nulovat. Pokud není watchdog softwarově nulovaný, resetuje automaticky celý procesor. To může být způsobeno například zamrznutím firmware. O automatické nulování se stará Byzance knihovna.

## Nastavení

Vlastnosti watchdogu se dají konfigurovat z command režimu bootloaderu. K tomu slouží položky ''wdenable'' a ''wdtime'. Povolené hodnoty wdenable jsou 0 \(vypnuto\) a 1 \(zapnuto - výchozí\), defaultní hodnota je wdtime je 30 \(v sekundách\). Defaultní hodnoty jsou nastavovány \[\[bootloader:defaults\|příslušným souborem bootloaderu\]\].

