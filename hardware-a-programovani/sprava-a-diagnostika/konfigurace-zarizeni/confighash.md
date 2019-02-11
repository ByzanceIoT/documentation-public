# Confighash

Confighash je speciální položka, která se automaticky přegeneruje po určitých změnách na zařízení. Umožňuje přeskočit automatický synchronizační proces se servery, čímž se zrychlí start a šetří se přenesená data. Confighash je užitečný v situaci,  kdy se zařízení odpojilo a připojilo k serverům a během tohoto času se žádné nastavení, ani další softwarové parametry nezměnily.

## Položky generující nový confighash

Veškeré [nastavení MQTT](../omezeni-konfigurace/mqtt.md).

Veškeré změny v [lowpan přihlašovacích údajích](../omezeni-konfigurace/lowpan.md).

Následující důležité [změny v binárkách](../omezeni-konfigurace/binarky.md):

* úspěšná aktualizace binárky firmware
* úspěšné obnovení binárky firmware
* libovolná úspěšná změna binárky bootloaderu
* libovolná úspěšná změna binárky backupu
* obnovení výchozího nastavení

Téměř všechny položky [konfigurace ](../omezeni-konfigurace/konfigurace.md)nastavovatelné z Portálu.

