# Identifikace zařízení

Všechny zařízení IODA mají ve FLASH paměti svého mikrokontroléru STM32 z výroby naprogramovaný **jedinečný identifikátor čipu**. Jedná se o 96 bitů dlouhé číslo reprezentované **24 hexadecimálními ASCII znaky**. Vyskytuje se na specifické adrese v paměti (liší se podle rodiny mikrokontroléru) a lze ho pouze číst. Toto číslo je Byzance interně označováno jako **Full ID**.

Každé zařízení dále umožňuje nastavit vlastní **Alias**, který uživateli ulehčí začízení identifikovat ve vlastní síti.

## Full ID

Je 96b číslo je pro naše účely převedeno na pole **24 ASCII znaků, reprezentovaných v hexadecimálním formátu**. Reprezentujeme ho bez oddělení pomlčkami nebo čárkami. Full ID se zapisuje **velkými písmeny**. Např. ''0123456789AB0123456789AB''. Lze to teoreticky přirovnat například k MAC adrese - ta je 48b dlouhá a zapisuje se jako šestice dvojciferných hexadecimálních čísel oddělených pomlčkami nebo dvojtečkami (např. ''01-23-45-67-89-AB'' nebo ''01:23:45:67:89:AB'').

#### Jak zjistit Full ID

Online v sekci Projects -> Hardware

![](/images/hardware/fullid.png)

Na zařízení přímo z [[bootloader:overview|bootloaderu]] výpisem přes [[tutorial:serial|sériovou linku]] nebo [[tutorial:usb|USB]].

![](/images/hardware/fullid_bootloader.png)


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

![](/images/hardware/full_id_code.png)




## Alias

Alias slouží společně s [Full ID](full-id.md) k identifikaci zařízení.

Narozdíl od Full ID, které je vždy unikátní z výroby a strojově dobře čitelné, Alias je nastavovaný uživatelsky pro lepší identifikaci člověkem. Při více zařízeních by měl být identifikátor Alias dostatečně popisný. Například při použití v osvětlení by měl Alias nést názvy typu "SVETLO-KUCHYN", "SVETLO-OBYVAK" a podobně. S identifikátorem Alias je možné pracovat několika způsoby.

**Omezení:**

* Alias může mít maximálně 63 znaků \(resp. 64 znaků včetně terminační nuly\)
* Může nabývat libovolné ASCII hodnoty včetně mezer
* Musí být [tisknutelný z pohledu C++](http://www.cplusplus.com/reference/cctype/isprint/)

# Jak s Alias pracovat?

Je možné jej zjistit při startu zařízení vyčtením při startu [bootloaderu](/byzance_documentation/hardware_intro/features/bootloader.md).

![alias_bootloader](/images/alias_bootloader.png)

Je možné jej zjistit či nastavit v [command režimu bootloaderu](/byzance_documentation/hardware_intro/features/bootloader/command-rezim.md). V případě nastavení z bootloaderu není garantována funkčnost, protože zařízení při startu zařízení žádá o nastavení Aliasu a v případě, že je název s Tyrionem kolizní, za správnou variantu je považovana varianta Tyrionu.

Alias je možné také zjistit v rámci uživatelského kódu dotazem pomocí [Byzance API](/byzance_documentation/hardware_intro/API/byzance-api.md) funkcí ''Byzance::get\_alias\(\);''.

Jednoduchý kód může vypadat například takto:

```cpp
#include "byzance.h"

Serial    pc(SERIAL_TX, SERIAL_RX); // tx, rx

void init(){
    pc.baud(115200);
}

void loop(){
    pc.printf("alias=%s\n", Byzance::get_alias());
    Thread::wait(500);
}
```

Jediná správná možnost editace aliasu je pomocí Byzance Code \(Becki\). V sekci hardware uživatele je možné Alias jak zjistit, tak změnit.

![alias_edit](/images/alias_edit.png)



