# Omezení MQTT

## MQTT

Připojení zařízení k serverům Byzance využívá technologii MQTT.

{% page-ref page="../../konektivita/komunikace-s-portalem.md" %}

Z hlediska bezpečnosti se používá hlavní a záložní MQTT server.

{% page-ref page="../../konektivita/prepinani-mezi-servery.md" %}

### **normal\_mqtt\_hostname**

Hostname nebo IP adresa hlavního serveru. Změna se projeví při dalším připojení k serveru.

| typ | char\[128\] |
| :--- | :--- |
| omezení | tisknutelné ASCII znaky zakončené terminační nulou |
| výchozí hodnota | main.homer.byzance.cz |
| možnost číst | ano, uživatel |
| možnost nastavit | ano, uživatel |
| confighash | ano |

### **normal\_mqtt\_port**

MQTT port hlavního serveru. Změna se projeví při dalším připojení k serveru.

| typ | 16 bit unsigned integer |
| :--- | :--- |
| omezení | 0 - 65535 |
| výchozí hodnota | 1881 |
| možnost číst | ano, uživatel |
| možnost nastavit | ano, uživatel |
| confighash | ano |

### **backup\_mqtt\_hostname**

Hostname nebo IP adresa záložního serveru. Změna se projeví při dalším připojení k serveru.

| typ | char\[128\] |
| :--- | :--- |
| omezení | tisknutelné ASCII znaky zakončené terminační nulou |
| výchozí hodnota | backup.homer.byzance.cz |
| možnost číst | ano, uživatel |
| možnost nastavit | ano, uživatel |
| confighash | ano |

### **backup\_mqtt\_port**

MQTT port záložního serveru. Změna se projeví při dalším připojení k serveru.

| typ | 16 bit unsigned integer |
| :--- | :--- |
| omezení | 0 - 65535 |
| výchozí hodnota | 1881 |
| možnost číst | ano, uživatel |
| možnost nastavit | ano, uživatel |
| confighash | ano |

### **mqtt\_username**

Přihlašovací jméno do MQTT brokeru. Změna se projeví při dalším připojení k serveru.

| typ | char\[48\] |
| :--- | :--- |
| omezení | tisknutelné ASCII znaky zakončené terminační nulou |
| výchozí hodnota | user |
| možnost číst | uživatelsky ne, pouze interně |
| možnost zapisovat | ano, uživatel |
| confighash | ano |

### **mqtt\_password**

Přihlašovací heslo do MQTT brokeru. Změna se projeví při dalším připojení k serveru.

| typ | char\[48\] |
| :--- | :--- |
| omezení | tisknutelné ASCII znaky zakončené terminační nulou |
| výchozí hodnota | pass |
| možnost číst | uživatelsky ne, pouze interně |
| možnost zapisovat | ano, uživatel |
| confighash | ano |

