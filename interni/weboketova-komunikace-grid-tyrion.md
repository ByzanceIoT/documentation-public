 ## Prvky komunikace Grid <-> Tyrion ### 

  - **Vývojová adresa:** (běžně localhost vývojáře) 
  - **Produkční verze:**  tyrion.byzance.cz

Připojení: 

Adresu na kterou se má mobilní zařízení - respektive každý terminál připojit dostane zařízení po API dotazu. Adresa je svázaná s Grid programem, který na mobilním zařízení běží. Ke stringu adresy se připojuje identifikátor terminálu, který je na začátku u nainstalovaných aplikací (iOS, Android) trvale přidělen (svázán s přihlášeným uživatelem) nebo v případě spuštění ve webové stránce se identifikátor přiděluje vždy na začátku komunikace. 
(Ukládání do cookies je zakázáno!)   

Dokumentace k API je zde. Vše co se týče Gridu na mobilních telefonech nebo v prohlížeči (všech terminálů) je v sekci APP-Api. 



### Získání M programu Gridu a adresy, na kterou se terminál připojí ### 
### Z QR kódu ###
QR kód je takzvaný m_program_token (060450da-4dca-4f45-816e-a13c85baa1f1)  identifikující právě jeden konkrétní program. 
```
  Dotaz: GET {url}/grid/m_program/app/token/{qr_token}
  Odpověď: Json, který obsahuje program i WebSocket adresu, ke které je potřeba přiložit identifikátor
  
  {
    "program": "string",
    "websocket_address": "string"
  }
```

### Z přihlášení 

```
  Dotaz: GET {url}/grid/m_program/app/m_programs
  Odpověď: Json, který obsahuje Grid programy - jeden z těchto programů si
           uživatel vybere a podle "qr_token" uděláš stejný API request jako vejš.  
  
```

-----
### Komunikační JSON Objekty Mezi GRID Terminálem a Homerem (Skrz Tyrion) 
  * Všechny Json Objekty určené pro komunikaci s Homerem budou okamžitě přeposlány na Homera (bez ohledu zda se jedná o Cloud nebo "RPI") 

  * Když se mobilní Terminál připojí a Homer bude taktéž připojený a bude to navíc "RPI" odešle mu server    následující objekt, kde mu předá parametry sítě, kde Homer běží a tyto parametry budou doručeny do terminálu (mobilu), který vyzkouší, zda se s konkrétním zařízením nemůže napojit napřímo. 
```
  {
    "dsafsdf" : "Asdfsdfas"
  }
```

------------------------------------------------------------

### Komunikační JSON Objekty Mezi GRID Terminálem a Tyrionem 

### M_Program je sice spojený, ale program pro Homera nikde neběží a není tedy co kam zasílat"
 * ```
 {
   "dsafsdf" : "Asdfsdfas"
 }
```
### V případě že se Terminál připojí k Tyrionovi, ale adresa připojení není validní
  * ```
 {
   "dsafsdf" : "Asdfsdfas"
 }
```

### V případě že Blocko Program není po připojení Terminálu k serveru taktéž připojeno 
  * Ve smyslu upozornění - sice si se k Tyrionovi připojil, vše funguje, ale nemáš komu posílat příkazy. ```
 {
   "dsafsdf" : "Asdfsdfas"
 }
```

### V případě že bylo ztraceno spojení s Blocko programem
  * Aby si uživateli oznámil, že se ztratilo spojení s Homerem (v cloudu nebo na RPI) ```
 {
   "dsafsdf" : "Asdfsdfas"
 }
```

### V případě že se homer připojil a navázal trvalé spojení
  * Aby si uživateli oznámil, že může aplikaci znovu požívat ```
 {
   "dsafsdf" : "Asdfsdfas"
 }
```

### V případě že proběhnul update M_programu
  * Přijde ti M_program (Grid program) který vázán s M_programem, na který si připojen.  ```
 {
   "dsafsdf" : "Asdfsdfas"
 }
```

### V případě že proběhnul update Blcoko Programu 
  * Přijde ti pouze upozornění, že byl blocko program updatován na homerovi. Pokud má uživatel nastaveno, že připojený M_Project (Skupina M Programů) se automaticky přepojí na nejnovější verzi nic závažného by se dít nemělo. Pokud tomu tak není. Nedovolím ti připojit se na novější Blocko program, protože verze M_Projectu má napevno spojení se starší verzí.      ```
 {
   "dsafsdf" : "Asdfsdfas"
 }
```

### V případě že bude probíhat Restart Tyrionu
  * Obsahuje informce zda bude probíhat restart v nejbližší době (aby si uživateli oznámil že to bylo řízén odpojení z důvodů updatu (z naší strany je to třeba Emergence stav pádu serveru - protože z posledního vzdechu tyrion spustí Emergence proceduru, kde všem oznámí svůj pád) Druhá varianta je že uživatele budeš informovat nějakou bublinou, že od 2AM do 4AM bude probíhat update. ```
 {
   "dsafsdf" : "Asdfsdfas"
 }
```
-----------------------------------------------------
### Odpovědi ze strany Tyriona na terminál po připojení ### 

### Terminál se snaží připojit na (B program), ale ten má už vyšší verzi (nahraná na Homerovi) a není dovoleno Temrinálu automaticky poskočit na vyšší verzi. ###

**Reply:**
```
 {
   "messageType"    : "invalidVersion",
   "message"        : "You are connecting to older version"
   "messageId"      : "SOME ID",
   "messageChannel" : "homer-server",
 }
```


### Terminál se připojit ke správně spárovanému M_Projektu s Blocko Programem - ale ten není nikde nahrán (Cloud nebo Local) ###

**Reply:**
```
 {
   "messageType"    : "notUploudedToHomer",
   "message"        : "???????"
   "messageId"      : "SOME ID",
   "messageChannel" : "homer-server",
 }
```

