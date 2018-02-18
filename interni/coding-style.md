## Coding style 

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
  
  
  