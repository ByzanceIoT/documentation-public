## Externí paměť mikrokontroléru

Velikost externí paměti na všech targetech je 8 MiB (32 Mb). Adresuje se od adresy 0. Z toho vyplývá rozsah

  * Začátek - 0x00000000
  * Konec - 0x00800000

Paměť je virtuálně rozdělena na několik sekcí. Jejich velikosti jsou následující:
  * Buffer - 0x00200000 (2 MiB). Slouží pro příjem binárky firmware při [[yoda:aktualizace_firmware|aktualizaci firmware]].
  * Backup - 0x00200000 (2 MiB). Sem se ukládá binárka, která prošla procesem ověření a bude sloužit jako záložní program pro případ selhání hlavního.
  * User   - 0x00200000 (2 MiB). Část přístupná uživateli.
  * Config - 0x001FD000 (2 MiB - 12 KiB). Konfigurační údaje.
  * Journal index - 0x00001000 (4 KiB). [[memory:journal|Index žurnálu]].
  * Journal data  - 0x00002000 (8 KiB). [[memory:journal|Data žurnálu]].

==== Rozložení paměti ====

Absolutní adresy na základě předchozího přehledu vypadají tedy následovně

```
     ============
    | 0x00000000 |
    |    ...     | (Buffer)
    | 0x001FFFFF |
    |============|
    | 0x08020000 |
    |    ...     | (Backup)
    | 0x003FFFFF |
    |============|
    | 0x08400000 |
    |    ...     | (User)
    | 0x085FFFFF |
    |============|
    | 0x08600000 |
    |    ...     | (Config)
    | 0x087FCFFF |
    |============|
    | 0x087FD000 |
    |    ...     | (Journal index)
    | 0x087FDFFF |
    |============|
    | 0x087FE000 |
    |    ...     | (Journal data)
    | 0x087FFFFF |
     ============
```

Pro nejlepší optimalizaci je třeba reflektovat [[memory:flash_tutorial| obecné informace o FLASH paměti]], které se ovšem trochu odchylují od obecného pustupu. Nejmenší jednotkou pro čtení je stránka (page), tedy 256 bytů dat. Nejmenší jednotkou zápisu (mazání) je subsektor o velikosti 4096 bytů. Více viz následující přehled:

```
#define SPIFLASH_SIZE             (uint32_t)8388608
#define SPIFLASH_SECTORS          (uint32_t)128
#define SPIFLASH_SECTOR_SIZE      (uint32_t)65536
#define SPIFLASH_SUBSECTORS       (uint32_t)2048
#define SPIFLASH_SUBSECTOR_SIZE   (uint32_t)4096
#define SPIFLASH_PAGES            (uint32_t)32768
#define SPIFLASH_PAGE_SIZE        (uint32_t)256
#define SPIFLASH_OTP_BYTES        (uint32_t)64
```

#### Mazání a zápis dat

Na základě výše uvedených informací začíná být zřejmý postup, jakým se zachází s daty. Pro změnu pár bytů dat je třeba provést následující kroky:
  * Je-li třeba změnit několik bytů, je možné je číst po stránkách o velikosti 256 bytů, ale zapisovat je nutné po subsektorech o 4096 bytech.
  * Proto je třeba načíst jeden subsektor po jednotlivých stránkách, tedy 16 iterací.
  * Tato stránka je uložena do RAM do vhodně velkého bufferu.
  * V RAM se změní se data, která jsou nutná změnit.
  * Smaže se příslušný subsektor ve FLASH.
  * Buffer z RAM se zapíše na místo smazaného subsektoru do FLASH.
  * Je-li třeba zapsat množství dat přesahující subsektor, či data která začínají a končí v jiných subsektorech, postup se opakuje.

Je zřejmé, že stejně jako při práci s interní pamětí může dojít ke ztrátě dat, pokud kód mikrokontroléru přestane odpovídat či dojde k výpadku napájení. Kritické místo je mezi kroky smazání subsektoru FLASH a zápisem bufferu z RAM. Tato situace je ovšem ošetřena [[memory:journal|využitím žurnálu]].

#### API pro přístup do externí paměti ====

```
/** Initialization of external memory
 *
 * @param settings
 * @param byz_spi
 * @return 0 - ok
 * @return !=0 - error
 */
static ExtMem_t init(struct external_spiflash *settings, ByzanceSpi * byz_spi);

/** This reads data from external memory
 *
 * @param	address
 * @param	offset
 * @param	data
 * @param	size
 * @return 0 - ok
 * @return !=0 - error
 */
static ExtMem_t read_data(uint32_t address, uint32_t offset, void *data, uint32_t size);

/** Write data to external memory
 *
 * @param address
 * @param offset
 * @param data
 * @param size
 * @param erase
 * @return ==0 - ok
 * @return !=0 - error
 */
static ExtMem_t write_data(uint32_t address, uint32_t offset, void *data, uint32_t size, bool erase = true);

/** Read data from external memory
 *
 * @param  offset
 * @param  data
 * @param  size
 * @return ==0 - ok
 * @return !=0 - error
 */
static ExtMem_t secure_write(uint32_t address, uint32_t offset, void * data, uint32_t size);

/** Erase the whole memory
 *
 * @param  none
 * @return ==0 - ok
 * @return !=0 - error
 */
static ExtMem_t erase(void);

/** Erase subsectors from given address to given address
 *
 * @param  start_index
 * @param  counter
 * @return ==0 - ok
 * @return !=0 - error
 */
static ExtMem_t erase_subsectors(uint32_t start_index, uint32_t counter);

/** Erase sectors from given address to given address
 *
 * @param  start_index
 * @param  counter
 * @return ==0 - ok
 * @return !=0 - error
 */
static ExtMem_t erase_sectors(uint32_t start_index, uint32_t counter);

/** Calculate index of the flash subsector belonging to given address
 *
 * @param  address
 * @return index or NULL if not initialized
 */
static uint32_t calculate_subsector_index(uint32_t address);

/** Calculate index of the flash sector belonging to given address
 *
 * @param  address
 * @return index or NULL if not initialized
 */
static uint32_t calculate_sector_index(uint32_t address);

/** Calculate index of the flash page belonging to given address
 *
 * @param  address
 * @return index or NULL if not initialized
 */
static uint32_t calculate_page_index(uint32_t address);

/** Calculate begin address of the flash subsector belonging to given address
 *
 * @param  address
 * @return subsector begin or NULL if not initialized
 */
static inline uint32_t calculate_subsector_begin(uint32_t address);

/** Calculate begin address of the flash sector belonging to given address
 *
 * @param  address
 * @return sector begin or NULL if not initialized
 */
static inline uint32_t calculate_sector_begin(uint32_t address);

/** Calculate begin address of the flash page belonging to given address
 *
 * @param  address
 * @return page begin or NULL if not initialized
 */
static inline uint32_t calculate_page_begin(uint32_t address);

/** Determine subsector size of flash memory
 *
 * @param  none
 * @return subsector size in bytes or NULL if not initialized
 */
static uint32_t get_subsector_size(void);

/** Determine sector size of flash memory
 *
 * @param  none
 * @return sector size in bytes or NULL if not initialized
 */
static uint32_t get_sector_size(void);

/** Determine page size of flash memory
 *
 * @param  none
 * @return page size in bytes or NULL if not initialized
 */
static uint32_t get_page_size(void);

/** Check external memory
 *
 * @param  none
 * @return ==0 - ok
 * @return !=0 - error
 */
static bool check_ok(void);
```

