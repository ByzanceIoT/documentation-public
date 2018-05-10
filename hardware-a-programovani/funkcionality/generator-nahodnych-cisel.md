# Náhodná čísla

Jazyk C++ disponuje metodou rand\(\), díky níž je možno generovat "náhodná čísla". Nejedná se ale o náhodná čísla v pravém slova smyslu. Vhodnější označení je "pseudonáhodná čísla".

Možným problémem pseudo-náhodných čísel či jejich posloupnosti je fakt, že po startu zařízení bude sekvence několika po sobě jdoucích čísel vypadat vždy stejně. 

Výstup následujícího kódu

```cpp
for(uint32_t i = 0; i<5; i++){
	printf("num = %d\n", rand()%256 );
}
```

bude po každém restartu vypadat například takto

```text
num = 45
num = 207
num = 70
num = 41
num = 4
```

Takové chování není úplně žádoucí, protože většinou je požadováno generovat unikátní náhodnou sekvenci čísel či unikátní jednotlivá čísla. Proto je třeba přidat využít náhodný seed.

## Použití seedu

Jazyk C++ nabízí možnost generovat náhodná čísla pomocí jiného klíče \(seedu\), než je výchozí. Díky tomu je dosažena skutečně náhodná sekvence po každém spuštění zařízení. K nastavení generátoru se využívá metoda srand\(\), jejímž argumentem je vhodně zvolené unikátní číslo.

Jak volit seed či jak vygenerovat skutečně náhodné číslo? Záleží na zvažovaném použití. Často doporučovaná metoda je použít jako seed unixové časové razítko. Tato varianta je pro většinu případů dostačující, ale má omezení v podobě nutnosti mít nastavený aktuální čas v zařízení, což nemusí být vždy garantováno. Například po prvním startu zařízení budou mít všechna zařízení časové razítko 0 a budou tedy generovat stejná náhodná čísla či jejich sekvence.

Další poměrně spolehlivou možností, jak získat náhodné číslo, je využít analogový šum. K tomu je nutný ADC převodník, připojený na libovolný podporovaný volný pin. Jedna z možných metod generování \(například\) 32 bitového čísla je 32 jednotlivých čtení z převodníku a skládání nejnižších bitů \(LSB\) do výsledného čísla. Tato metoda může být nevýhodná kvůli nutnosti využití ADC převodníku, ve většině případů se ale nejnižší bit výstupu z převodníku považuje za dostatečně náhodný. 

## Hardwarová jednotka

Nejspolehlivější metoda generování je využití hardwarové jednotky generátoru náhodných čísel \(TRNG - true random number generator\). Jednotku musí implementovat daný mikrokontrolér. U zařízení IODAG3E je jednotka přítomna a ve výchozím nastavení inicializována. 

Její podporu definuje makro MBEDTLS\_ENTROPY\_HARDWARE\_ALT a samotná implementace je součást balíku MBED TLS. Zdrojový kód pro vygenerování pěti čísel s použitím TRNG může být například následující

```cpp
#include "mbedtls/entropy_poll.h"

unsigned int seed;
size_t len;

#ifdef MBEDTLS_ENTROPY_HARDWARE_ALT
printf("hw entropy ENABLED\n");

for(uint32_t i = 0; i<5; i++){
	mbedtls_hardware_poll(NULL, (unsigned char *) &seed, sizeof seed, &len);
	printf("num_trng = %u\n", seed);
}
#else
printf("hw entropy DISABLED\n");
#endif
```

Takto generovaná čísla budou vždy unikátní. Další výhodou je, že jednotka TRNG potřebuje oproti rand\(\) knihovně zhruba polovinu času k vygenerování jednoho 32 bit čísla \(2.5us oproti 5us\).

