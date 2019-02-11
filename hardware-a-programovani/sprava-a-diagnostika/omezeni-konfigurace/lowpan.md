# Lowpan

### lowpan\_credentials

Nastavení přihlašovacích údajů k síti ve formátu `<název>-<klíč>`. Položka `<název>` může být až 16 znaků dlouhá; položka `<klíč>` je přesně 32 znaků dlouhá, přičemž povolené znaky jsou a-f, A-F a číslice 0-9. Při uložení se převede na 16 bytů dlouhé hexadecimální číslo. Změna se projeví po restartu zařízení.

### **keymanager\_name**

| char\[16\] |  |
| :--- | :--- |
| omezení | tisknutelné ASCII znaky zakončené terminační nulou |
| výchozí hodnota | byzance |
| možnost číst | ano, uživatel |
| možnost zapisovat | ano, uživatel |
| confighash | ano |

### **keymanager\_key**

| char\[16\] |  |
| :--- | :--- |
| omezení | tisknutelné ASCII znaky zakončené terminační nulou |
| výchozí hodnota | a0a1a2a3a4a5a6a7a8a9aaabacadaeaf |
| možnost číst | ano, uživatel |
| možnost zapisovat | ano, uživatel |
| confighash | ano |

