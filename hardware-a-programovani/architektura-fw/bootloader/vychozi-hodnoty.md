# Výchozí hodnoty

Každé zařízení je vybaveno detekcí[ validní konfigurace](../../sprava-a-diagnostika/konfigurace-zarizeni.md). Pokud konfigurace neodpovídá očekávaným parametrům, případně pokud je zařízení nové a nikdy nebylo nakonfigurováno, místo některých \(nebo všech\) položek mohou být automaticky dosazeny výchozí hodnoty.

Kontrola parametrů se děje vždy při vstupu do [bootloaderu](./), ještě před spuštěním vlastního firmware.

| parameter | value | user configurable |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| MQTT\_HOSTNAME | 192.168.65.179 | ✓ |
| MQTT\_PORT | 1881 | ✓ |
| MQTT\_USERNAME | user | ✓ |
| MQTT\_PASSWORD | pass | ✓ |
| FLASHFLAG | 0 | ✗ |
| AUTOBACKUP | 0 | ✓ |
| BLREPORT | 0 | ✓ |
| WDENABLE | 1 | ✓ |
| WDTIME | 30 | ✓ |
| NETSOURCE | ethernet | ✓ |
| CONFIGURED | 0 | ✓ |
| LAUNCHED | 0 | ✗ |
| ALIAS | BYZANCE | ✓ |
| BACKUPTIME | 60 | ✓ |
| WEBVIEW | 1 | ✓ |
| WEBPORT | 80 | ✓ |
| TIMEOFFSET | 0 | ✓ |
| TIMESYNC | 1 | ✓ |
| LOWPANBR | 0 | ✓ |
| RESTARTBL | 0 | ✓ |
| AUTOJUMP | 300 | ✓ |

