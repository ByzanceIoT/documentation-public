## Centrum notifikací


Notifikace jsou určeny pro Long-pull komunikaci výlučně mezi Tyrionem a Becki. Slouží k informování uživatele o stavech jeho prvků a úlohách, která mají delší trvání provedení. (Upload programu na Homer, Přihlášení Homera, auto update prvků atd..)  

Přihlášení k odběru probíhá přes protokol (Server-Sent Events) ([[https://github.com/markusjura/sse-chat-java | GIT inspirace]]) ("Pozor, není funkční v IE a SPARTAN a EDGE) Link zadokumentovaného endpointu připojení    [[http://swagger.byzance.cz/#!/Notifications/subscribe_notification|SWAGGER docu ]]. Swagger ale nedovoluje zdokumentování všeho a tak je směrodatná a nadřazená dokumentace ve WIKI. Pro otestování lze zavolat[[http://swagger.byzance.cz/#!/Notifications/sendSomething| testovací API ]]  

Pokud dochází k operaci, která je časově náročná - a frontend by čekal na odpověď delší dobu (déle než +-5 sekund, je na místě mu vrátit okamžitě odpověď o přijaté žádost "úlohy" a uživatele na Becki o stavu vykonání informovat skrze notifikaci. Popřípadě notifikaci použít jako upozornění, že došlo ke ztrátě spojení, někdo další v projektu udělal změnu atd.. V tomto případě stačí pouze zavolat metodu níže a ona se má o vše ostatní postarat.  


## Tyrion implementace

  * Skrze metodu (Zde jejich seznam)
   ```
        // Není implementovaná - Určeno pro pozdější využití!!! 
        NotificationController.send_notification(person, Notification_level.message, "zpráva");
        
        NotificationController.send_notification(person, Notification_level.success, "zpráva");
        NotificationController.send_notification(person, Notification_level.info,    "zpráva");
        NotificationController.send_notification(person, Notification_level.warning, "zpráva");
        NotificationController.send_notification(person, Notification_level.error,   "zpráva");
    </code>  je možno uživateli odeslat novou zprávu (notifikaci)- nezáleží zda je online nebo offline.
    
   

  * **Notification_level** je Enum objekt obsahující typ zprávy (info,success, warning, error, message) aby bylo zajištěno, že front-end bude vždy znát všechny typy zpráv.  
  
  * Odesláním zprávy na osobu se zajistí odeslání do všech jeho přihlášených terminálů. Pravděpodobně by se dalo přidat odeslání celé skupině, firmě, lidem v projektu atd.. 
 

=== Podoba zasílaných zpráv (Odesílání i příjímání) === 
  * level nabývá hodnot (info,success, warning, error, message) <code json>{
     "level"                 : "success", 
     "text"                  : "Samotná zpráva ",
     "confirmation_required" : "true",            // Vyžaduji RestApi potvrzení přečtení 
     "read"                  : "false",           //říká zda byla notifikace přečtena - Potvrzení pomocí Rest Api 
     "created"               : "1458315085"       // UNIX time stamp - Datum vytvoření   
}
```

* message určeno pro upozornění  na odeslanou zprávu ( bude upřesněno (není součást vyskakovací bubliny - Radku nebuď hnidopich :D )  