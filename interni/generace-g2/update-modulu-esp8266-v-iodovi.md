## Update modulu ESP8266 v Iodovi

Modul ESP8266 je v Yodovi napevno napájen. Pro manuální naprogramování po sériovce se musí modul přepnout do Update režimu.

 1. Do MCU Yody se nahraje program ESP_bridge z repozitáře ''hw-libs''. Tento program softwarově protuneluje sériovku vyvedenou na RPI spolu se sériovkou připojenou k WIFI čipu.

 2. Stiskne se USR tlačítko na Yodovi, které rozsvítí červenou LED na kitu. Tímto se WIFI modul přepne do update režimu (yoda správně nastaví piny WIFI modulu do režimu update). Wifi modul teď poslouchá na Wifi sériovce příkazy. Změna režimu (data/update) se zaloguje do RPI sériovky.

 3. Otevře se Arduino (nebo jiné) IDE s konkrétním WIFI projektem a vybuildí se WIFI binárka. Arduino IDE se nastaví na konkrétní COM port v PC, který je spojen s RPI sériovkou.

 4. Uploaduje se Arduino (nebo jiný) projekt do RPI sériovky, data se automaticky protunelují do WIFI.

 5. Po uploadu binárky se stiskne USR tlačítko, takže Yoda přepne WIFI modul zpět do normálního režimu. Alternativně stačí restartovat YODU.

HW nastavení ESP8266 modulu pro update (ani jedno z následujících není při update nutné řešit):

```
GPIO0  pullup na 3V3
GPIO2  pullup na 3V3
EN     pullup na 3V3
NRST   pullup na 3V3

GPIO15 pullup na GND
```

Postup udate
```
Postup update:
1) napájení trvale připojené
2) Zapojit RST na GND, poté GPIO0 na GND
3) Odpojit (odzemnit) v MCU RST, poté odzemnit GPIO0 (oba zůstanou viset na pullupech v 3V3)
4) start v upgradovací utilitě
Normálně je GPIO0 a reset pullupem vytažený na 3V3.
```