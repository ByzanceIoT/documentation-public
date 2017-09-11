# Softwarový restart

Zařízení je možné na dálku softwarově restartovat.

Zařízení takovýto požadavek zaregistruje a okamžitě volá funkci pomocí Byzance API napojenou na ''Byzance::attach\_restart\_follows''. Zde se uživatel dozví o příchozím požadavku na restart. Ne vždy je restart žádoucí, proto je možné vyvolat jeho odložení. K tomu slouží funkce ''Byzance::restart\_postpone\(time\_t sec\)''.

Příklad možného použití

```cpp
void init(){

    Byzance::attach_restart_follows(&my_function);

}

void my_function(){

    // nejaka logika na zjisteni, jestli mi restart vadi nebo ne
    
    // pokud vadi, o kolik se ma posunout
    
    Byzance::restart_postpone(cislo);

}
```

Dotazování na stav restartu je možné i periodicky funkcí ''Byzance::restart\_pending\(\)'', jejíž návratovou hodnotou je čas, kolik zbývá do restartu.

Více informací je na stránce \[\[tutorial:public\_functions\|veřejných funkcí Byzance\]\].

