---
search:
    keywords: ['RGB_matrix', 'Init', 'set_color', 'set_background', 'set_pixel', 'put_char', 'put_line', 'put_row', 'paint', 'paint_all', 'detach_ticker', 'attach_ticker']
---

# class RGB\_matrix

T��da ovl�daj�c� maticov� RGB diplej. 
## Public Static Functions

|Type|Name|
|-----|-----|
|static void|[**Init**](class_r_g_b__matrix.md#1a1bf32e59aebd0f71dae7e4d7df873a33) (PinName Pin\_R1, PinName Pin\_R2, PinName Pin\_G1, PinName Pin\_G2, PinName Pin\_B1, PinName Pin\_B2, PinName Pin\_CLK, PinName Pin\_LAT, PinName Pin\_OE, PinName Pin\_A, PinName Pin\_B, PinName Pin\_C, PinName Pin\_D) |
|static void|[**set\_color**](class_r_g_b__matrix.md#1a0b0efc012d447edbddb96d8010d14738) (char color) |
|static void|[**set\_background**](class_r_g_b__matrix.md#1a3730975e93180ab12b0c4d3feaaddfec) (char color) |
|static void|[**set\_pixel**](class_r_g_b__matrix.md#1a0f5a43c8ca7923cd50635ed91b271922) (uint16\_t x, uint16\_t y, uint16\_t c) |
|static char|[**put\_char**](class_r_g_b__matrix.md#1a4f1994b6322c463bb01ca77a2392e393) (int x, int y, char c) |
|static void|[**put\_line**](class_r_g_b__matrix.md#1ab79c20364f712d782c53386d318f7848) (char \* str, int line\_number) |
|static void|[**put\_row**](class_r_g_b__matrix.md#1a9c14fedf5bedb865a84d2f1b17c0ac81) (char \* str, uint16\_t mins, int line\_number) |
|static void|[**paint**](class_r_g_b__matrix.md#1a7f229b5b1013120b0013a5537135f228) () |
|static void|[**paint\_all**](class_r_g_b__matrix.md#1abef4d4bc0ec8d3ee44d665bd4e8e7ca7) () |
|static void|[**detach\_ticker**](class_r_g_b__matrix.md#1af6fb20fecd7e0cda21d4c31ff0719bea) () |
|static void|[**attach\_ticker**](class_r_g_b__matrix.md#1a36463416e219823dff078f9d52c38074) () |


## Public Static Functions Documentation

### function <a id="1a1bf32e59aebd0f71dae7e4d7df873a33" href="#1a1bf32e59aebd0f71dae7e4d7df873a33">Init</a>

```cpp
static void RGB_matrix::Init (
    PinName Pin_R1,
    PinName Pin_R2,
    PinName Pin_G1,
    PinName Pin_G2,
    PinName Pin_B1,
    PinName Pin_B2,
    PinName Pin_CLK,
    PinName Pin_LAT,
    PinName Pin_OE,
    PinName Pin_A,
    PinName Pin_B,
    PinName Pin_C,
    PinName Pin_D
)
```


Inicializuje RGB display, 

**Parameters:**


* _V�stupn�_ piny pomoc� kter�ch bude za��zen� diplay ovl�dat

Inicializuje knihovnu **[RGB\_matrix](class_r_g_b__matrix.md)** a fyzick� piny desky. Z�rove� zapne ticker, kter� sekven�n� vykresluje ��dky displeje 

### function <a id="1a0b0efc012d447edbddb96d8010d14738" href="#1a0b0efc012d447edbddb96d8010d14738">set\_color</a>

```cpp
static void RGB_matrix::set_color (
    char color
)
```


Nastav� barvu, kterou bude display p�i dal��ch v�pisech pou��vat 

**Parameters:**


* _ENUM_ RGB\_MATRIX\_COLOR 



### function <a id="1a3730975e93180ab12b0c4d3feaaddfec" href="#1a3730975e93180ab12b0c4d3feaaddfec">set\_background</a>

```cpp
static void RGB_matrix::set_background (
    char color
)
```


Nastav� barvu, kterou bude display p�i dal��ch v�pisech pou��vat v pozad� 

**Parameters:**


* _ENUM_ RGB\_MATRIX\_COLOR 



### function <a id="1a0f5a43c8ca7923cd50635ed91b271922" href="#1a0f5a43c8ca7923cd50635ed91b271922">set\_pixel</a>

```cpp
static void RGB_matrix::set_pixel (
    uint16_t x,
    uint16_t y,
    uint16_t c
)
```


Nastav� barvu na konkr�tn�m pixelu 

**Parameters:**


* _pozice_ x - ��dek 
* _pozice_ y - sloupec 
* _c_ - barva pixelu (0-7, 0 = zhasnuto) 



### function <a id="1a4f1994b6322c463bb01ca77a2392e393" href="#1a4f1994b6322c463bb01ca77a2392e393">put\_char</a>

```cpp
static char RGB_matrix::put_char (
    int x,
    int y,
    char c
)
```


Vykresl� znak z knihovny znak� na danou pozici (pozice ur�ena od lev�ho horn�ho rohu) 

**Parameters:**


* _pozice_ x - ��dek 
* _pozice_ y - sloupec 
* _c_ - znak kter� se m� vykreslit 



### function <a id="1ab79c20364f712d782c53386d318f7848" href="#1ab79c20364f712d782c53386d318f7848">put\_line</a>

```cpp
static void RGB_matrix::put_line (
    char * str,
    int line_number
)
```


Vyp�e zadan� text na zadan� ��dek (1-4). 

**Parameters:**


* _\*str_ pole char� k v�pisu (doporu�uji pracovat se datov�m typem string a p�i vol�n� funkce do argumentu zadat &str[0]) 
* _line\_number_ - ��dek na kter� se text vyp�e 



### function <a id="1a9c14fedf5bedb865a84d2f1b17c0ac81" href="#1a9c14fedf5bedb865a84d2f1b17c0ac81">put\_row</a>

```cpp
static void RGB_matrix::put_row (
    char * str,
    uint16_t mins,
    int line_number
)
```


Vyp�e zadan� text na zadan� ��dek (1-4). 

**Parameters:**


* _\*str_ pole char� k v�pisu (doporu�uji pracovat se datov�m typem string a p�i vol�n� funkce do argumentu zadat &str[0]) 
* _mins_ po�et min vypsan�ch vpravo matice 
* _line\_number_ - ��dek na kter� se text vyp�e 



### function <a id="1a7f229b5b1013120b0013a5537135f228" href="#1a7f229b5b1013120b0013a5537135f228">paint</a>

```cpp
static void RGB_matrix::paint ()
```


metoda kter� sekven�n� vykresl� jeden ��dek. Tato funkce je sama vol�na tickerem ka�d�ch 500 mikrosekund po inicializaci a nen� pot�eba j� volat v u�ivatelsk�m k�du. 

### function <a id="1abef4d4bc0ec8d3ee44d665bd4e8e7ca7" href="#1abef4d4bc0ec8d3ee44d665bd4e8e7ca7">paint\_all</a>

```cpp
static void RGB_matrix::paint_all ()
```


Vykresl� v�echny ��dky 

### function <a id="1af6fb20fecd7e0cda21d4c31ff0719bea" href="#1af6fb20fecd7e0cda21d4c31ff0719bea">detach\_ticker</a>

```cpp
static void RGB_matrix::detach_ticker ()
```


Funkce odpoj� ticker pou��van� k sekven�n�mu vykreslov�n� ��dk� 

### function <a id="1a36463416e219823dff078f9d52c38074" href="#1a36463416e219823dff078f9d52c38074">attach\_ticker</a>

```cpp
static void RGB_matrix::attach_ticker ()
```


Funkce znovu p�ipoj� ticker, pou��van� k sekven�n�mu vykreslov�n� ��dk� 



----------------------------------------
The documentation for this class was generated from the following file: `D:/w/hw-libs/\_libs\_/libraries/RGB\_matrix.h`
