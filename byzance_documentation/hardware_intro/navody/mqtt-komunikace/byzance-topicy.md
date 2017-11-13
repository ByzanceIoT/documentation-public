## Byzance topicy 

#### Digital IN/OUT 

Digitální zpráva IN nemá v payloadu JSON, ale pouze jednu ASCII hodnotu rovnou 0/1, t/f, nebo T/F.

Digitální zpráva OUT FIXME doplnit

#### Analog IN/OUT 

Analogová zpráva IN nemá v payloadu JSON, ale pouze ASCII číslo, které se potom v zařízení pomocí funkce ''atof'' převede na binární číslo reprezentující příslušnou hodnotu, které se následně předá v callbacku zaregistrované funkci.

Analogová zpráva OUT funguje analogicky FIXME doplnit

==== Message IN/OUT ====

FIXME doplnit