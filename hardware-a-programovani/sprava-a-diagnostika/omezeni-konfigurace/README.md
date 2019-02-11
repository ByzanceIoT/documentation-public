# Omezení konfigurace

Každé zařízení je vybaveno detekcí [validní konfigurace](https://docu.byzance.cz/hardware-a-programovani/sprava-zarizeni/konfigurace-zarizeni). Pokud konfigurace neodpovídá očekávaným parametrům, případně pokud je zařízení nové a nikdy nebylo nakonfigurováno, místo některých \(nebo všech\) položek mohou být automaticky dosazeny výchozí hodnoty.

Kontrola parametrů se děje vždy při vstupu do [bootloaderu](https://docu.byzance.cz/hardware-a-programovani/architektura-fw/bootloader), ještě před spuštěním vlastního firmware.

## Ostatní

### \*\*\*\*

### lowpan\_credentials

Nastavení přihlašovacích údajů k síti ve formátu `<název>-<klíč>`. Položka `<název>` může být až 16 znaků dlouhá; položka `<klíč>` je přesně 32 znaků dlouhá, přičemž povolené znaky jsou a-f, A-F a číslice 0-9. Změna se projeví po restartu zařízení.

