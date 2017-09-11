# Watchdog

Watchdog je vlastnost mikrokontroléru, která se zapíná a konfiguruje v Bootloaderu.

Pokud je watchdog zapnutý a nastavený na určitý čas, musí se pravidelně softwarově resetovat. Pokud není watchdog softwarově resetovaný, resetuje automaticky celý procesor. To může být způsobeno například zamrznutím firmware.

## Nastavení

Vlastnosti watchdogu se dají konfigurovat z command režimu bootloaderu. K tomu slouží položky ''watchdog\_enabled'' a ''watchdog\_time''. Povolené hodnoty watchdog\_enabled jsou 0 a 1 \(default\), defaultní hodnota je watchdog\_time je 30 \(v sekundách\). Defaultní hodnoty jsou nastavovány \[\[bootloader:defaults\|příslušným souborem bootloaderu\]\].

