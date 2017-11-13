## Vývojářské příkazy pro Homera 


Vývojář potřebuje lokálního Homera, aby mohl provádět experimenty a programovat nové funkce.''Neformátovat (zdrojový kód)''
Homer se dá stáhnout z GITu.

Pro správnou funkci je třeba udělat následující
  * Stáhnout repozitář
  * V Terminálu zadáme npm install (vždy po každem updatu z repozitáře) 

### Režim plnohodnotné konfigurace

(Neohrožuje soustavu produkčních serverů) 

     Na MacOS v Terminálu **npm start** 
     Na Windows **./homer-server --config config/default_config.json**

Režim vývojáře hotová základní konfigurace (Neohrožuje soustavu produkčních serverů). Na portu localhost:3000 vznikne webová stránka - kde uživatel vizuálně může vytvořit vlastní konfiguraci. (Připojit Homera na Tyriona atd.) 
Pozor, jakmile se server nakonfiguruje vyžaduje oprávnění (user a password - tedy funkčního tyriona!)   

     Na MacOS v Terminálu **npm run dev_mode** 
     Na Windows **./homer-server --config config/developer_config.json**

### Vlastní Config 
 
Existuje složka config a v ní json soubory. Můžete si vytvořit vlastní konfigurační soubor a volat si ho příkazem 
./homer-server --config config/muj_sobor.json

### Dokumentace používání Homera 

Dokumentace jak co ovládat není vázaná na wiki zde - ale na dokumentaci uvnitř homera (jednodušeji se spravuje a je vždy aktuální vůči verzi kterou požíváte) Dokumentaci najdete na webové stránce Homera po jeho zapnutí na localhost:3000 v menu Dokumentace. 