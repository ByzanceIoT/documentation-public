## Identifikátor zařízení 


Všechny námi používané mikrokontroléry STM32 mají ve FLASH paměti z výroby naprogramovaný jedinečný identifikátor čipu. Jedná se o 96 bitů dlouhé číslo. Vyskytuje se na specifické adrese v paměti (liší se podle rodiny mikrokontroléru) a je pouze ead-only. Toto číslo je Byzance interně označováno jako ''Full ID''

Toto 96b číslo je pro naše účely převedeno na pole **24 ASCII znaků, reprezentovaných v hexadecimálním formátu**. Reprezentujeme ho bez oddělení pomlčkami nebo čárkami. Full ID se zapisuje **velkými písmeny**. Např. ''0123456789AB0123456789AB''. Lze to teoreticky přirovnat například k MAC adrese - ta je 48b dlouhá a zapisuje se jako šestice dvojciferných hexadecimálních čísel oddělených pomlčkami nebo dvojtečkami (např. ''01-23-45-67-89-AB'' nebo ''01:23:45:67:89:AB'').

#### Jak zjistit Full ID 

Online v sekci Projects -> Hardware
{{ :hardware:fullid.png?direct&200 | fullid_online }}

Na zařízení přímo z [[bootloader:overview|bootloaderu]] výpisem přes [[tutorial:serial|sériovou linku]] nebo [[tutorial:usb|USB]].
{{ :hardware:fullid_bootloader.png?direct&200 | fullid_bootloader }}

Pomocí [[tutorial:public_functions|veřejné metody]] třídy Byzance ''Byzance::get_full_id()'' výpisem přes [[tutorial:serial|sériovou linku]] nebo [[tutorial:usb|USB]].

```
#include "byzance.h"

Serial	pc(SERIAL_TX, SERIAL_RX); // tx, rx

void init(){
    pc.baud(115200);
}

void loop(){
    pc.printf("full_id=%s\n", Byzance::get_full_id());
    Thread::wait(500);
}
```

{{ :hardware:full_id_code.png?direct&200 | full_id_code}}


