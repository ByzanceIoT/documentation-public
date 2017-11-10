# Alias

Alias slouží společně s \[\[hardware:full\_id\|Full ID\]\] k identifikaci zařízení. Narozdíl od Full ID, které je vždy unikátní z výroby a strojově dobře čitelné, Alias je nastavovaný uživatelsky pro lepší identifikaci člověkem. Při více zařízeních by měl být identifikátor Alias dostatečně popisný. Například při použití v osvětlení by měl Alias nést názvy typu "SVETLO-KUCHYN", "SVETLO-OBYVAK" a podobně. S identifikátorem Alias je možné pracovat několika způsoby.

Omezení

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

