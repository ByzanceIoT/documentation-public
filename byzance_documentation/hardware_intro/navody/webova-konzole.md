## Webová konzole 

Průběh vykonávání uživatelského programu je možné logovat pomocí webové konzole. Je implementována jako statická třída, funguje automaticky od začátku běhu programu a obsahuje následující veřejné metody dostupné uživateli.

```cpp
// zalogování erroru
static bool error(const char* format, ...);

// zalogování warningu
static bool warn(const char* format, ...);

// zalogování info
static bool info(const char* format, ...);

// zalogování logu
static bool log(const char* format, ...);

// je konzole aktivovaná?
static bool enabled();
```
### Vlastnosti konzole

Fukkce **error**, **warning**, **info** a **log** slouží k logování různých úrovní různých vlastních událostí, parametricky jsou shodné s C/C++ fukcí [[http://www.cplusplus.com/reference/cstdio/printf/| printf]]. Logy konzole se automaticky přenášejí do webového rozhraní Becki pomocí protokolu [[Yoda:MQTT|MQTT]], kde zařízení může uživatel sledovat. Návratovou hodnotou fukncí konzole je možné detekovat, jestli informace dorazila do webového rozhraní.

Fukce **enabled** slouží k zjištění, jestli je logování do webové konzole zapnuto. Logování se automaticky vypíná, pokud logy nikdo neodebírá. Je možné logy archivovat a odebírat, do budoucna asi za poplatek FIXME doplnit pak.