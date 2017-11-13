## Nasazení homer-js na Azure 

Tento dokument popisuje jak nasadit homer-js na Azure. Předpokládá se, že se homer-js poprvé nainstaluje a pak se jen upgraduje. Proto první sekce popisuje upgrade a až druhá sekce popisuje postup počáteční instalace.

### Upgrade na aktuální verzi 

  - Nahrát požadovanou verzi homer-js
  - Spustit ''npm install''

### Detailně

  - Otevřít [[sysadmin:sprava:azure_app_service#otevreni_konzole|konzoli dané service]] (např. //Byzance-Homer//)
  - Zadat příkaz ''cd site/homer-js''
  - Zadat příkaz ''git fetch origin''
  - Zadat příkaz ''%%git reset --hard <tag>%%'' (např. //v0.0.1//)
  - Zadat příkaz ''%%git clean -dxf%%''

Nyní několik kroků, které obchází [[sysadmin:problemy#npm_install_git_ssh_v_azure|nějaký bug]] a které snad časem nebudou nutné:

    - Pokud bude potřeba upgrade Blocko:
    - Zadat příkaz ''cd ../blocko''
    - Zadat příkaz ''git fetch origin''
    - Zadat příkaz ''%%git reset --hard <tag>%%'' (např. //v0.1.0//)
  - Změnit referenci na //blocko// v souboru ''homer-js/package.json'' na ''%%file://D:\\home\\site\\blocko%%''

Nyní už klasicky:

  - Zadat příkaz ''cd ../homer-js''
  - Zadat příkaz ''npm install''

### První instalace 

Tato sekce je důležitá jen pro toho, kdo poprvé nasazuje homer-js na Azure. Následně už stačí jen upgradovat. Postup v kostce je následující:

  - Vytvořit novou instanci Azure App Service
  - Nakonfigurovat IIS, aby spouštělo homer-js
  - Nahrát požadovanou verzi homer-js
  - Spustit ''npm install''

### Vytvoření nové instance Azure App Service 

  * jako jméno použít např. //Byzance-Homer//
  * zároveň udělit přístup do repozitářů ''homer/homer-js'' a ''js-components/blocko''
  * viz [[sysadmin:instalace:azure_app_service|sysadmin:instalace:azure_app_service]]

### Konfigurace service 

[[https://tomasz.janczuk.org/2011/08/hosting-nodejs-applications-in-iis-on.html|zdroj]] [[https://www.iis.net/configreference/system.webserver|zdroj]]

  - V adresáři ''publishUrl/site/wwwroot'' (viz. [[#vytvoreni_nove_instance_azure_app_service|výše]]) vytvořit tyto soubory:
  
  ```
#!/usr/bin/env node
var HomerServerBuilder = require("../homer-js/js/HomerServerBuilder");
new HomerServerBuilder.HomerServerBuilder()
    .setMoscaServer(1883)
    .setTyrionWsService("ws://tyrion.byzance.cz/websocket/blocko_server/Alfa")
    .getResult();
    </code><code xml web.config>
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.webServer>
    <defaultDocument>
      <files>
        <clear />
        <add value="server.js" />
      </files>
    </defaultDocument>
    <handlers>
      <add name="iisnode" path="server.js" verb="*" modules="iisnode" />
    </handlers>    
  </system.webServer>
</configuration>
    ```

### Nasazení homer-js 

  - Otevřít [[sysadmin:sprava:azure_app_service#otevreni_konzole|konzoli dané service]] (např. //Byzance-Homer//)
  - Zadat příkaz ''cd site''
  - Zadat příkaz ''git clone -b <tag> git@git.byzance.cz:homer/homer-js.git'' (např. //v0.0.1//)

Nyní několik kroků, které obchází [[sysadmin:problemy#npm_install_git_ssh_v_azure|nějaký bug]] a které snad časem nebudou nutné:

  - Zadat příkaz ''git clone -b <tag> git@git.byzance.cz:js-components/blocko.git'' (např. //v0.1.0//)
  - Změnit referenci na //blocko// v souboru ''homer-js/package.json'' na ''%%file://D:\\home\\site\\blocko%%''

Nyní už klasicky:

  - Zadat příkaz ''cd homer-js''
  - Zadat příkaz ''npm install''