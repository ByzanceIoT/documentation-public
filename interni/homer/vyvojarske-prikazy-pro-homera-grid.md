## Vývojářské příkazy pro Homera (GRID)

Vývojář Gridu potřebuje aktivního lokálního Homera, aby mohl provádět experimenty a programovat nové funkce. Homer se dá stáhnout z GITu.
Pro správnou funkci je třeba udělat stejné začátečnické procedury co vývojáři HW. (Viz zde [[homer:commands|Vývojářské příkazy pro Homera]]
Zapnout Homera, připojit ho k Tyrionovi a ověřit že svítí zeleně na úvodní stránce. 

### Grid APP 

Websocket klient se k serveru připojuje na speciální 2xUUID adrese kterou mu přidělí po přihlášení Tyrion. 
(Pomocí Rest Api - Viz dokumentace na swagger.byzance.cz) 


### Varianta A: 
- uživatel přijde na stránku grid.byzance.cz 
  - Grid App zobrazí uživateli přihlašovací obrazovku  
  - Uživatel se pomocí Rest-Api přihlásí (Login viz [[http://swagger.byzance.cz/#!/APP-Api/login|Login - shodný s klasickým]]) Veškeré další Api je podepisováno tímto tokenem z Tyriona který se vrátil.  
  - Grid App si zaregistruje Token viz [[http://swagger.byzance.cz/#!/APP-Api/get_identificator|Swagger]] Cokoliv přes websocket kde to bude vyžadováno (s Homerem) je vše podepisováno s **"terminal_token"** 
  - Uživatel si vybere ze seznamu viz [[http://swagger.byzance.cz/#!/APP-Api/get_M_Project_all_forTerminal|Swagger]]
  - Grid požádá o URL k přihlášení viz [[http://example.com|Swagger]] k vybranému programu ve vybrané instanci!!! (Grid program může být pod několika instancemi - proto jsou vyžadovány tři ID!! (instance_id a  m_program_id a version_object_id)!) 
  - Tyrion vrátí program ve stringu + url adresu  kam se může Grid App připojit - tento token má ale jednorázové použití. A při každé ztrátě spojení je nutné si nechat vygenerovat nové. Každý token má životnost 5s. Procedura viz předchozí krok. 
  - Grid se připojí k homer serveru na adresu kde musí nahradit proměnou #token za přihlášený verifikovaný token z předchozího kroku 
  ```ws://pridelena_url/dloooouhyUUID/#token``` 
  - Komunikuje s Homerem (ten mu muže vnutit nové příkazy jako nahrátí nového programu atd.) Viz uvedení příkazy níže.
  - Token je uložen v paměti Homera - Homer si jeho platnost ověřuje u Tyriona. V případě pádu spojení má Aplikace 5-15 NA ZNOVUPŘIPOJENÍ. A token je validní - po této době je vyžadováno aby se aplikace ověřila znovu.
  - Tyrion také ověřuje kdo se připojuje - Token může být Public nebo vázaný na uživatele.
       

### Varianta B:  
- uživatel dostane grid.byzance.cz/gggg555AAAdddAAAdddaa odkaz na aplikaci v (QR atd) - takový program to musí umět už sám od sebe (podle flag registru)    
  - Grid App si zaregistruje Token pomocí [[http://example.com|Swagger]] - v cookies není jen token uživatele - ale i tak jde pak připojení v administraci deaktivovat. 
  - Grid App požádá Tyriona o URL na Homera 
  - Tyrion vrátí url adresu kam se může Grid App připojit - tento token má ale jednorázové použití. A při každé ztrátě spojení je nutné si ho nechat vygenerovat nové. (Nebo v časové odchylce 5-15 sekund, kterou Homer má v RAM)  Každý token má životnost 5-15s po vygenerování. Procedura viz předchozí krok. Tento token je nutný i u programu, které nejsou "privátní"
  - Grid se připojí k homer serveru na ws:/ pridelena_url/token adresu
  - Grid App požádá Tyriona o program s použitím tokenu v URL [[http://example.com|Swagger]]
  - Komunikuje s Homerem (ten mu muže vnutit nové příkazy jako nahrátí nového programu atd.) Viz uvedení příkazy níže.




### WebView APP 

U každé instance i B_Programu, který to podporuje je vracen parametr "instance_remote_url" 
Obsahuje přesnou adresu ws://homer_server.byzance.cz:8942/uuid___uuid/#token 

Parametr #token je třeba nahradit za API Token, který se běžně používá pro rest-api komunikaci s Tyrionem! 
 

