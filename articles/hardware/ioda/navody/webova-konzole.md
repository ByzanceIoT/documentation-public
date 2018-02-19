# Webová konzole

Průběh vykonávání uživatelského programu je možné logovat pomocí webové konzole.

Jejím smyslem je možnost nahrazení klasické sériové linky. Její výstup je možné najít v Portálu Byzance v záložce Hardware, vždy v konfiguraci konkrétního zařízení.

![](/assets/console.PNG)

# Výhody a nevýhody

Výhodou webové konzole je, že je díky ní možno monitorovat libovolné zařízení na dálku, či si vypisovat průběhy kódu. Není nutná fyzická přítomnost zařízení a připojení k počítači USB kabelem, či použití FTDI převodníku. Odpadají problémy s instalací driveru sériové linky, nastavení baud rate, parity a dalších.

Nevýhodou je, že vyžaduje, aby bylo zařízení stále připojeno k internetu. Dalším problémem může být fakt, že příliš velké množství logů může velmi zpomalovat běh programu, zvláště při pomalém připojení.

# Použití

Konzole je implementována jako statická třída, funguje automaticky od začátku běhu programu \(není nutná její inicializace\) a obsahuje následující veřejné metody dostupné uživateli.

```cpp
// je konzole zapnutá? (tj., odebírá ji někdo v Portálu?)
static bool enabled();




// zalogování erroru
static bool error(const char* format, ...);

// zalogování warningu
static bool warn(const char* format, ...);

// zalogování info
static bool info(const char* format, ...);

// zalogování logu
static bool log(const char* format, ...);
```

Jednoduchý příklad kódu, který využívá Konzoli může být například takovýto

```cpp
ukázkový program
```

# Vlastnosti konzole

Fukce **error**, **warning**, **info** a **log** slouží k logování různých úrovní různých vlastních událostí, parametricky jsou shodné s C/C++ fukcí [printf](http://www.cplusplus.com/reference/cstdio/printf/). Logy konzole se automaticky přenášejí do webového rozhraní Becki pomocí protokolu [MQTT](/articles/hardware/komunikace-se-servery.md), kde zařízení může uživatel sledovat. Návratovou hodnotou je možné detekovat, jestli informace dorazila do webového rozhraní.

Fukce **enabled** slouží k zjištění, jestli je logování do webové konzole zapnuto. Logování se automaticky vypíná, pokud logy nikdo neodebírá.

