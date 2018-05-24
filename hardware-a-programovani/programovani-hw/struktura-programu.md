# Struktura programu

Zařízení Byznce se programují v jazyce **C++** a využívají [**MBED API**](https://os.mbed.com/docs/latest/reference/apis.html) a [**Byzance API**](byzance-api/). Pro správnou funkčnost programu je nutné na první řádek nejprve importovat knihovnu "byzance.h" příkazem

```cpp
#include "byzance.h"
```

Tato knihovna má za úkol automaticky inicializovat periferie, připojit zařízení k internetu a inicializovat vlákna, která se starají o [aktualizaci firmware](../architektura-fw/aktualizace-fw.md) a připojení k serverům. Importem knihovny se také zpřístupní funkce [Byzance API](byzance-api/) a [uživatelská makra](byzance-api/uzivatelska-makra.md).

## Definice fyzických vstupů a výstupů

Po importu všech potřebných knihoven je možno začít používat objekty definované v knihovnách. Může se jednat o vytvoření konstuktorů, periferie, nebo fyzické [vstupy a výstupy](../hardware/zakladni-jednotky/iodag3e/rozhrani-a-periferie.md), které se budou v programu používat.

```cpp
// Definice fyzických vstupů a výstupů
DigitalOut DI1(X02);
DigitalIn DO1(X05);
AnalogOut AO1(Y23);
AnalogIn AI1(Y22)
```

Další informace je možno naleznout v sekci [MBED API](mbed-api/).

## Definice virtuálních vstupů a výstupů

Při programování funkčního bloku nástroji BLOCKO v portálu Byzance je často potřeba definovat virtuální vstupy a výstupy, které symbolizují právě vstupy a výstupy funkčního bloku ven ze zařízení. Tyto definice je nutné zanést společně s fyzickými vstupy a výstupy.

```cpp
// digitalni vstup s nazvem din_name
DIGITAL_INPUT(din_name, {
    my_din_variable = value;
})

// analogovy vstup s nazvem ain_name
ANALOG_INPUT(ain_name, {
    my_ain_variable = value;
})
```

Bližší informace o významu a funkci virtuálních vstupů/výstupů a jejich programování je možno naleznout v příslušné kapitole.

{% page-ref page="byzance-api/vstupy-a-vystupy-do-portalu.md" %}

## Definice komunikačních rozhraní

Pokud je v programu potřeba využít nějaké komunikační rozhraní jako Sériová linka, SPI, CAN apd. je vhodné provést jejich definici v této části za definicí vstupů a výstupů. Definice sériové linky je znázorněna v následujícím kódu.

```cpp
Serial pc(SERIAL_TX_pin, SERIAL_RX_pin); // tx, rx
```

Bližší informace ke komunikačním rozhraním lze získat v sekci [MBED API-Komunikační rozhraní](mbed-api/komunikacni-rozhrani.md)

## Hlavní funkce programu

Program může mít definované tři základní funkce

* pre\_init\(\)
* init\(\)
* loop\(\)

### Funkce pre\_init\(\)

Tato funkce je zavolána na začátku programu jako první, ještě předtím, než je inicializováno vlákno Byzance a předtím než se zařízení připojí k serverům. Tuto funkci není povinné implementovat, nicméně její implementace může být užitečná například při debugu komunikace se servery nebo ovládání některých funkcí inicializovaných operačním systémem MBED.

```cpp
void pre_init(){

}
```

### Funkce init\(\)

Funkce _init_ je provedená hned po funkci _pre\_init_ a stejně tak pouze jednou. Tato funkce slouží k inicializaci prvků potřebných v hlavní části programu. Její implementace není povinná.

```cpp
void init(){
    pc.printf("Hello world\n");
}
```

### Funkce loop\(\)

Poslední hlavní funkcí je funkce _loop_, Tato funkce je vykonávaná ve smyčce a nahrazuje tak funkci _while\(true\)_. Jediným rozdílem je to, že mezi jednotlivými smyčkami se dává prostor Byzance vláknu, které zajišťuje komunikaci a resetuje se watchdog.

```cpp
void loop(){
    pc.printf("Hello world\n");
    Thread::wait(500);
}
```

## Hello world

Následující kód zobrazuje strukturu programu **Hello\_world** s definicí vstupů, výstupů a komunikačních rozhraní a implementací všech třech hlavních funkcí

```cpp
#include "byzance.h"

// Definice fyzických vstupů a výstupů
DigitalOut DO1(X02);
DigitalIn DI1(X05);
AnalogOut AO1(Y23);
AnalogOut AI1(Y22);

Serial pc(SERIAL_TX, SERIAL_RX); // tx, rx

void init(){
    // Hello world se vypise jednou pri startu
    pc.printf("Hello world from init function\n");
}

void loop(){
    // Hello world se bude vypisovat stale dokola kazdych 500 ms
    pc.printf("Hello World\n");
    Thread::wait(500);
}
```

