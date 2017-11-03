## LED signalizace IODAG3E 

LED signalizace je implementována s využitím LED modulu. V defaultním nastavení bez zásahu uživatele **slouží k vizuální reprezentaci stavů zařízení**. Funkci LED modulu lze přeprogramovat vlastní funkcionalitou. Tato generace použivá k signalizaci stavu jednu RGB LED diodu. Stavy jsou proto dány jako kombinace blikání a barvy.


### Signály

Známe sekvence pro pro IODUG3E:

##### Stav CONNECTED

* Yoda úspěšně připojený a subscribovaný k Homerovi
* rychlé blikání se střídou 50 - 200ms zap, 200ms vyp
* barva: LED_COLOR_GREEN

##### Stav DISCONNECTED

* Yoda není připojen/subscribovaný k Homerovi
* pomalé blikání s převahou rozsvícení 2 sekundy zap, sekunda vyp
* barva: LED_COLOR_GREEN

##### Stav BUSY
* Probíhá upload nové binárky, popř. záloha aktuální
* rychlé blikání se střídou 50% 200ms zap, 200ms vyp
* barva: LED_COLOR_VIOLET

##### Stav ERROR/DEAD
- LED modul bliká červeně
- Většinou fatalita, totální selhání nějaké komponenty, problém s pamětí, chyba která nikdy neměla nastat a podobně

### Signalizace Bootloaderu

* Při vstupu do bootloaderu se na RGB modulu rozsvítí **žlutá barva**.
* Pokud je třeba přepnout bootloader do command režimu, podrží se tlačítka USER a RESTART a poté se pustí RESTART. Zhruba po vteřině se zapne command režim, přičemž LED modul se přepne do **modré barvy**, kde trvale svítí. V té chvíli je nutné pustit i tlačítko USER.
* Pokud se v bootloaderu začne vykonávat časově náročnější operace (typicky flashování firmware, záloha atd.), bootloader přeblikává **žlutě**.

