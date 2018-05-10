# Struktura programu

Zařízení Byznce se programují v jazyce **C++** a využívají knihoven **MBED API** a **Byzance API**. Pro správnou funkčnost programu v Byzance zařízení je nutné importovat knihovnu Byzance API příkazem

```cpp
#include "byzance.h"
```

Tato knihovna má za úkol automaticky inicializovat periferie, připojit zařízení k internetu a inicializovat vlákna, která se starají o update zdrojového kódu a připojení k serverům. Importem knihovny se také zpřístupní [funkce](https://github.com/byzance/public-documentation/tree/38b460c46404c197299c0f0a84e3402a9b74c8d7/programovani/byzance-api/funkce.md) a [uživatelská makra](https://github.com/byzance/public-documentation/tree/38b460c46404c197299c0f0a84e3402a9b74c8d7/programovani/byzance-api/uzivateska-makra/README.md) Byzance API.

## Definice fyzických vstupů a výstupů

Následně po importu všech potřebných knihoven, je v případě jejich použití nutné definovat fyzické vstupy a výstupy, které se budou v programu používat. Zařízení Byzance na své GPIO sběrnici disponují Analogovými i digitálními vstupy a výstupy.

```cpp
// Definice fyzických vstupů a výstupů
DigitalOut DI1(X02);
DigitalIn DO1(X05);
AnalogOut AO1(Y23);
AnalogIn AI1(Y22)
```

Bližší informace o fyzických vstupech a výstupech lze získat v [MBED API - Vstupy a výstupy](mbed-api/vstupy-a-vystupy.md).

## Definice virtuálních vstupů a výstupů

Při programování funkčního bloku toolu [BLOCKO](https://github.com/byzance/public-documentation/tree/38b460c46404c197299c0f0a84e3402a9b74c8d7/programovani/odkaz%20na%20blocko/README.md) v portálu Byzance je často potřeba definovat virtuální vstupy a výstupy, které symbolizují právě vstupy a výstupy funkčního bloku. Tyto definice je nutné zanést společně s fyzikými vstupy a výstupy.

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

Bližší informace o významu a funkci virtuálních vstupů/výstupů a programování funkčních bloků lze dohledat v sekci [Prograování funkčních bloků](vstupy-a-vystupy-do-portalu.md)

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

void pre_init(){
    //Funkce pre_init - proběhne právě jednou
}

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

