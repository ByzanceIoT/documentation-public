## Topic Report


Tento topic je trošku speciální, protože Yoda na něm neposlouchá, ale pouze do něj reportuje události, které by mohly být zajímavé pro Homera. Zprávy neobsahují message ID a Yoda nečeká na jejich potvrzení.

### Yoda je připojen 
Pokud se Yoda úspěšně připojí k brokerovi, prohlásí se za připojeného.
Pokud se k němu i subscribuje, prohlásí se za subscribovaného.

Jestli Yoda ještě nedokončil subscribovací proceduru, zahazuje všechny možné příchozí packety. Až je procedura dokončena, vyšle Homerovi uvítací zprávu a teprve potom začne poslouchat jeho požadavky.

Uvítací zpráva je odeslána do topicu
''XXXXXXXXXXXXXXXXXXXXXXXX/report_out/connected'' a obsahem je JSON.

```
{
  "device"     : "FULL_ID"
}
```

### State 

Zpráva je odeslána do topicu
''XXXXXXXXXXXXXXXXXXXXXXXX/report_out/state'' a obsahem je JSON.

Slouží k oznámení změny stavu některé vnitřní komponenty Yody.

Komponenty můžou být 4 typy: bootloader, firmware, backup, buffer
Stavy každé komponenty můžou být taky 4: invalid, valid, erasing, erased

Při tvorbě zálohy Yoda například změní stav komponenty "backup" na "invalid" a po dokončení na "valid".
Při update binárky se změní "buffer" z původního stavu na "erasing" a poté na "erased".

```
{
  "component"         : "state"
}
```