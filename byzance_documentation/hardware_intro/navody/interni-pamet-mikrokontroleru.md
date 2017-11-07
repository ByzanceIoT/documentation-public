## Interní paměť mikrokontroléru

#### Práce s interní pamětí 
Je-li třeba pracovat s interní pamětí mikrokontroléru, čtení je poměrně triviální. Data lze číst po bytech přímo z konkrétní požadované adresy. Zápis se ale trochu komplikuje. Paměť je rozdělená na jednotlivé stránky, které jsou u Cortex M0 fixní, většinou o velikosti 2KiB, u Cortex M4 architektury se však velikosti výrazně liší. 

#### Rozdělení sektorů 

Většina mikrokontrolérů Cortex M4 má stránky paměti rozdělené takto
  * Sektor 0-3   -> 16 KB
  * Sektor 4     -> 64 kB
  * Sektor 5-11  -> 128 kB

Pokud je paměť složena z více paměťových bank (např. interní flash 2MiB je nejčastěji 2x1MiB), pattern rozdělení sektorů se opakuje
  * Sektor 12-15 -> 16 KB
  * Sektor 16    -> 64 kB
  * Sektor 17-23 -> 128 kB

Uživatelská práce s interní pamětí se nedoporučuje, protože může dojít k poškození firmware nebo bootloaderu. Výše uvedené skutečnosti je třeba reflektovat (především při mazání, kde se může stát, že je třeba smazat jenom několik bytů dat, ale technologie FLASH smaže celou stránku společně i s jinými daty).

#### Rozsahy adres 


YODAG2
  * Velikost celkem 512 KiB (0x00080000) - celkem 8 sektorů
  * Z toho bootloader 64 KiB (0x00010000) - sektory 0 - 3
  * Z toho firmware 448 KiB (0x00070000) - sektory 4 - 7

YODAG3E
  * Velikost celkem 2 MiB (0x00200000) - celkem 24 sektorů
  * Z toho bootloader 64 KiB (0x00010000) - sektory 0 - 3
  * Z toho firmware 1984 KiB (0x001F0000) - sektory 4 - 23

```
     ============
    | 0x08000000 |
    |    ...     | (Bootloader, 64 KiB in total)
    | 0x0800FFFF |
    |============|
    | 0x08010000 |
    |    ...     | (Size depending on target)
    |    end     |
     ============
```

#### API pro přístup k interní paměti 

```
/** Initialize and unlock internal memory
 *
 * @param  none
 * @return none
 */
static IntMem_t	init(void);

/** Erase internal memory.
 *
 * !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
 *    Be careful when using this function.
 *    It doesnt't only erase given memory form start to end
 *    but WHOLE PAGE where this address belongs.
 *    It can cause unwanted data loss.
 * !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
 *
 * @param	start 	begin address
 * @param	end		end address
 * @return	TODO: implement properly
 */
static IntMem_t erase(uint32_t StartAddress, uint32_t EndAddress);

/** Read from internal memory
 *
 * @param	address	address to read
 * @param	offset	offset from address to read
 * @param	data	pointer to source data buffer
 * @param	size	size of data to read
 * @return	TODO:	implement properly
 */
static IntMem_t	read_data(uint32_t address, uint32_t offset, void *data, uint32_t size);

/** Write to internal memory
 *
 * @param	address	address to write
 * @param	offset	offset from address to write
 * @param	data	pointer to result data buffer
 * @param	size	size of data to write
 * @param	erase	auto-erase memory before write
 * 					leave blank or true if you are not sure
 * 					or read erase warning
 *
 * @return	TODO:	implement properly
 */
static IntMem_t write_data(const uint32_t address, const uint32_t offset, const void *data, const uint32_t size, const bool erase = true);
```