## Coding style 

#### C++ coding standard 

Verze: **v0.1-beta**

----------

#### Příklad 

#### FooURLParser.h 

```
#ifndef FOO_URL_PARSER_H
#define FOO_URL_PARSER_H

#ifndef FOO_URL_PARSER_MAX_SIZE
#define FOO_URL_PARSER_MAX_SIZE (size_t)256
#endif

typedef struct {
   int begin_index;
   int end_index;
} ParserConfig;

enum class ParserStrategy : uint8_t {
    Unknown,
    Fast = 0xFF,
    Slow = 0x77,
};

class FooURLParser {

public:
    FooURLParser(char *file_path, ParserStrategy strategy, int begin_index = 0, int end_index = 256, int port_number = 55);
    ~FooURLParser();

    size_t file_size();

    bool is_done();

    static bool is_parser_ready(char *file_path);

    uint32_t public_size = 0;

protected:
    size_t _size = 0;
    uint32_t _index = 0;
    char *_file_path = NULL;
    ParserStrategy _strategy = ParserStrategy::Unknown;
    ParserConfig _config = {};

    PinPort _pinPort;

    void private_parsing_loop(size_t loop_index);

    size_t max_size() {
        return FOO_URL_PARSER_MAX_SIZE;
    }

};

#endif // FOO_URL_PARSER_H
```

==== FooURLParser.cpp ====

<file cpp FooURLParser.cpp>

```
#include "FooURLParser.h"

#define FOO_URL_PARSER_PRIVATE_SIZE_LIMIT (size_t)32

FooURLParser::FooURLParser(char *file_path, ParserStrategy strategy, int begin_index, int end_index, int port_number) : _config{begin_index, end_index}, _pinPort(port_number) {
    _file_path = file_path;
    _strategy = strategy;

    private_parsing_loop(_index);
}

FooURLParser::~FooURLParser() {
    _size = 0;
}

size_t FooURLParser::file_size() {
    if (_size > (max_size() - FOO_URL_PARSER_PRIVATE_SIZE_LIMIT)) {
        return max_size();
    }
    return _size;
}

bool FooURLParser::is_done() {
    return (_size == _index);
}

bool FooURLParser::is_parser_ready(char *file_path) {
    return (_index == 0 && fs_is_file_exist(file_path));
}

void FooURLParser::private_parsing_loop() {
    uint32_t i = 0;
    for (;i < FOO_URL_PARSER_PRIVATE_SIZE_LIMIT; ++i) {
        _index++;
    }
}

```

#### Pravidla 

##### Názvy souborů 

  * **Název souboru** koresponduje s **názvem třídy** uvnitř souboru
  * Soubor by měl obsahovat **pouze jednu třídu**, max. **enum**-y, **struct**-ury **typedef**-y související s dannou třídou

##### Třídy 

  * Název tříd se pojmenovávají **PascalCase**-em (UpperCamelCase) s tím že zkraty obsahují všechna písmena velká (např. //FooURLParser//)
  * Hlavičkový soubor obsahuje **ifndef konstrukci** s názvem třídy **UPPER_CASE**-em doplňenou o _H (//<nowiki>#ifndef FOO_URL_PARSER_H .. #define FOO_URL_PARSER_H .. #endif // FOO_URL_PARSER_H</nowiki>//)
  * V **hlavičkovém souboru** jsou **implementovány pouze metody u kterých je to nezbytené** (např. závisí na vnějším nastavení define - viz. metoda //size_t max_size()// )
  * Běžně na "**private**" proměnné a metody používáme **protected** .. pouze pokud chceme něco **vědomně** vyloženě **private**, používáme **private**
  * Pokud chceme **pouze statickou třídu** (všechny metody jsou static), přesouváme **konstruktor a destrukotor do private nebo protected** sekce
  * Všechny **private** a **protected** proměnné prefixujeme znakem '**_**'
  * **Public** proměnné žádný **prefix nemají** (viz. //public_size//)

##### Metody 

  * **Metody ve třídě** se pojmenovávají **lower_case**-em stejně tak jako **názvy jejich paramterů**
  * Metody se **pojmenovávají stejně** ať jsou **static**, **public**, **private** i **protected**
  * V hlavičkovém souboru **můžeme definovat** paramterům **výchozí hodnoty**

#### Enum 

  * **enum**-y vytváříme pomocí konstrukce **enum class** .. ideálně **definujeme i datový typ** (v příkladu //ParserStrategy : uint8_t//)
  * **Použití** těchto probíhá **včetně názvu enum**-u (např. //ParserStrategy::Fast//)
  * Název **enum**-u stejně tak jeho hodnot je **PascalCase**-em (UpperCamelCase)
  * Pokud **enum** souvisí s **více než jednou třídou** měl by být **definován ve vlastním hlavičkovém souboru**

##### Define 

  * **define** se pojmenovávají **UPPER_CASE**-em
  * V **hlavičkovém souboru** by měli být **pouze define které lze zvenku změnit** a měli by mít konstrukci pro **defaultní hodnotu** popř. **vyhodit chybu při nedefinování**.
  * **define** potřebné **pouze pro implementaci** by měli být **v *.cpp souboru**
  * **Pozor** na použití zvenčí **změnitelných define v *.cpp souboru** - kompilované *.cpp soubory se ukládají do cahce a proto tyto define mohou mít chybnou hodnotu

##### Struct 

  * **struct**-ury vytváříme pomocí konstrukce **typedef struct {...} StuctName;**
  * **Jméno struct**-ury je pojmenováno pomocí **PascalCase** (UpperCamelCase)
  * **Jména vlastností** ve struktuře jsou pomenovány pomocí **lower_case**

##### Ostatní 

  * Na **velikosti** používáme **size_t** datový typ
  * **výpočty a přiřazení s mezerou**, tj. správně //cntr += array[i];// nebo //array[i] = 'a';//. Špatně jsou zápisy //cntr+=array[i];// nebo //array[i]='a';//. S mezerami je kód přehlednější.

##### TODO 

  * promyslet použití namespace
  * typedef
  
  
  