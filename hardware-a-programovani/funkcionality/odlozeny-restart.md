# Odložený restart

Zařízení je možné na dálku softwarově restartovat.

Zařízení takovýto požadavek zaregistruje a okamžitě volá funkci pomocí Byzance API napojenou na ''Byzance::attach\_restart\_follows''. Zde se uživatel dozví o příchozím požadavku na restart. Ne vždy je restart žádoucí, proto je možné vyvolat jeho odložení. K tomu slouží funkce ''Byzance::restart\_postpone\(time\_t sec\)''.

Příklad možného použití

```cpp
void init(){

    Byzance::attach_restart_follows(&my_function);

}

void my_function(){

    // some logic which can postpone waiting restart

    Byzance::restart_postpone(seconds);

}
```

Dotazování na stav restartu je možné i periodicky funkcí ''Byzance::restart\_pending\(\)'', jejíž návratovou hodnotou je čas v sekundách, které zbývají do restartu.

Více informací v příslušné části dokumentace.

{% page-ref page="../programovani-hw/byzance-hardware-api.md" %}



