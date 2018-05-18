# GSM

 \#TODO nějaký obrázek IODA + BTS + Internet + portál + eventuelně další IODa přes lowpan

Zařízení IODA lze připojit do Internetu pomocí buňkové sítě GSM. Toto je realizováno pomocí [GSM shieldu](../hardware/rozsirujici-moduly/gsm-shield.md). 

Pro využití připojení je nutné [specifikovat zdroj internetu](specifikace-zdroje-internetu.md) jako GSM. Dále je nutné využít buď integrovanou eSIM nebo vlastní mini SIM. SIM musí být být nastavena tak, aby nevyžadovala PIN kód. 

Další parametry jsou určeny operátorem. Ve výchozí konfiguraci se používá následující konfigurace APN:

* **APN**: internet
* bez uživatelského jména a hesla

Toto výchozí nastavení pokrývá všechny české operátory. Pokud operátor vyžaduje speciální nastavení APN, dle MCC a MNC kódu operátora je proveden pokus o zjištění APN, uživatelského jména a hesla z předpřipravené tabulky. 

