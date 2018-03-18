#Proces aktualizace


Pokud je třeba aktualizovat některou z komponent Ioda, je třeba provést následující kroky
  * IODA se musí připravit na příjem nové binárky. V tomto kroku probíhá většinou mazání sekce ''buffer'', je-li to třeba. Tento krok se nazývá **prepare**.
  * Nahrátí samotné binárky do IODA - proces **upload**. Binárka se v této chvíli uloží do sekce ''buffer''.
  * Aktualizace příslušné komponenty binárkou uloženou v sekci ''buffer''. Krok se nazývá **update**.

Komponenta může být následující
  * firmware - hlavní program
  * bootloader - bootloader zařízení
  * backup - záložní program

## Proces upload 

V rámci procesu upload probíhá nahrávání binárky z Cloudu do sekce ''buffer'' zařízení. Tento postup je odolný proti výpadku internetového připojení - pokud dojde k poškození přenášených dat či k výpadku, data v sekci ''buffer'' budou automaticky označena za neplatná a není je možné potom nasadit jako jednu z hlavních komponent.

## Proces update 

Až je binárka nahraná v Iodovi, ještě je stále třeba ji z externí paměti překopírovat na určité místo, což může být například hlavní firmware, bootloader nebo backup.

### Komponenta firmware
Pokud je updatována komponenta firmware, automaticky se zapne signalizátor ''flashflag''  spravovaný bootloaderem a po volitelném restartu **bootloader** provede přeflashování hlavního programu z externí paměti ''buffer'' do interní ''firmware''.

### Komponenta backup nebo bootloader
Pokud má být updatována záloha nebo bootloader, kopírování z ''buffer'' do ''backup'' nebo ''bootloader'' se provede v **hlavním firmware** bez nutnosti restartu zařízení.



![](/assets/img_20180316_204757.jpg)

