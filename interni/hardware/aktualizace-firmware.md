## Aktualizace firmware 


Pokud je třeba aktualizovat některou z komponent Yody nebo Device, je třeba provést 2 sady kroků.
  * Nahrát binárku do Yody (**upload**). Binárka se při nahrátí uloží do sekce ''buffer''.
  * Aktualizovat s binárkou z bufferu příslušnou komponentu (**update**).

Komponenta může být následující
  * firmware - hlavní program zařízení
  * bootloader - bootloader zařízení
  * backup - záložní hlavní program. Úzce spjato s [[feature:autobackup| funkcí autobackup]].

Pokud je třeba do zařízení binárku nahrát, je třeba poslat správnou sekvenci příkazů do [[Yoda:topic_commands| topicu commands]] a řídit se případně [[errorcodes:errorcodes|chybovými kódy]].

#### Proces upload 

Příkazy mají následující posloupnost
  * upload/start
  * upload/data (opakováno tolikrát, kolik je partů binárky)
  * upload/end

Podrobnější specifikace příkazů je v sekci [[Yoda:topic_commands| MQTT Topic Commands]]

#### Proces update 

Až je binárka nahraná v Yodovi, ještě je stále třeba ji z externí paměti překopírovat na určité místo, což může být například hlavní firmware, bootloader, backup, nebo device firmware a device backup.

Pro aktualizaci je třeba poslat příslušné příkazy do topicu
  * update/start
  * upload/status (volitelně)
  * system/restart (volitelně)

Pokud je updatována komponenta firmware, zapne se navíc proměnná ''flashflag'' a po volitelném restartu **bootloader** provede přeflashování hlavního programu z externí paměti do interní. Pokud má být updatována záloha nebo bootloader, toto se provede v **hlavním firmware**.

Podrobnější specifikace **update** příkazů je v sekci [[Yoda:topic_commands| MQTT Topic Commands]].
