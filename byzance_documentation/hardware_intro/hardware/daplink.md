## DAPLINK

Jedná se o otevřený projekt, který si klade za cíl vytvořit univerzální programátor/debugger, projekt je hostován na  [github Daplink](https://github.com/mbedmicro/DAPLink)|]]. Mezi hlavní přednosti patří:
  * drag and drop programování - nahrávání binárních dat do FLASH paměti cílového procesoru
  * převodník sériové linky USB <-> UART
  * debugger (gdb klient)

{{ :tutorial:daplink.png?600 | Blokové schéma Daplink}}

Z hlediska hardwarové a softwarové architektury je třeba rozlišit programující a programovaný mikroprocesor. Programující mikroprocesor (na obrázku konkrétně LPC11U35) má za úkol komunikovat s PC prostřednictvím sběrnice USB a vytvořit virtuální sériový port, MSD zařízení (vyměnitelný disk), případně GDB klienta. Pro programování programovaného mikroprocesoru využívá SWD/JTAG rozhraní, dále nabízí piny RX a TX virtuálního sériového portu. Z hlediska programovaného mikroprocesoru není Daplink univerzální - **jeden konkrétní firmware pro programující MCU je kompatibilní pouze s jedním nebo užší množinou programovaných MCU** - závislost na flashovacím algoritmu, oblasti RAM, velikost a pozice paměti flash aj..

===== Softwarová architektura =====
Z hlediska softwaru je celý Daplink prozatím založen především na projektech Keil uVision 5. Jednotlivé projekty (kombinace board + target) jsou zapsány v souboru ''projects.yaml'', příklad záznamu:
<code>
lpc11u35_byzanceg3_if:
    - *module_if
    - *module_hic_lpc11u35
    - records/board/byzanceg3.yaml
</code>
Je patrné, že je využito společných modulů a modulů pro programovací procesor LPC11U35. Dále je definován odkaz na desku ''byzanceg3.yaml'', jeho obsah může být následující:
<code>
common:
    sources:
        board:
            - source/board/byzanceg3.c
        target:
            - source/target/st/stm32f437/target.c
            - source/target/st/target_reset.c

</code>

Veškeré ''*.yaml'' soubory slouží python skriptu pro generování uVision projektů. V případě klonování Daplink z githubu je potřeba nejdříve generovat uVision projekty pomocí python skriptu nebo bat souboru ve složce tools. Ve skriptech lze také provést změny, kterými je možné generovat makefily pro arm-gcc-none-eabi*, v současnosti ovšem nelze projekty tímto překladačem kompilovat.

Soubor ''byzanceg3.c'' je velmi jednoduchý - obsahuje ID desky (mělo by být v rámci Daplink unikátní a přidělené správci projektu). V sekci target je definován cílový procesor: ''target_reset.c'' obsahuje pomocné funkce pro odemčení FLASH paměti aj. (ty nejsou využity).

Soubor ''stm32f437/target.c'' má následující strukturu:
<code c>
#include "target_config.h"

// The file flash_blob.c must only be included in target.c
#include "flash_blob.c"

// target information
target_cfg_t target_device = {
    .sector_size    = 0x4000,
    .sector_cnt     = (0x200000 / 0x4000),
    .flash_start    = 0x08000000,
    .flash_end      = 0x08200000,
    .ram_start      = 0x200001AC,
    .ram_end        = 0x20030000,
    .flash_algo     = (program_target_t *) &flash,		
    .erase_reset    = 1,
};
const uint32_t firmware_start_address = 0x08010000;

</code>
Je zde tedy potřeba nastavit oblast začátek a konec paměti FLASH a RAM a dále je třeba uvést odkaz na strukturu popisující přístup k paměti FLASH. Dále byla přidána globální konstantní proměnná, která definuje začátek oblasti určené pro firmware.

Vlastní programování probíhá následovně:
  * uživatel zahájí přenos binárního souboru na připojený flash disk
  * programující mikroprocesor detekuje pokus o vytvoření nového souboru na filesystému
  * programující mikroprocesor restartuje programovaný mikroprocesor a do jeho paměti RAM nahraje spustitelný program
  * programující MCU přijímá data po USB a postupně je předává pomocí programovacích pinů programu běžícímu v paměti RAM programovaného mikroprocesoru
  * programovaný mikroprocesor přijatá data postupně ukládá do své FLASH pamětí a na vyžádání maže sektory
  * programování je hotovo
Program, který má běžet v paměti RAM programovaného mikroprocesoru je znám již při kompilaci projetu a je zapsán v souboru ''flash_blob.c'' (jeho inkluze je v souboru ''target.c'') a může vypadat následovně:
<code c>
#include "flash_blob.h"
#define RAM_OFFSET 0x1AC

static const uint32_t output_flash_prog_blob[] = {
    0xE00ABE00, 0x062D780D, 0x24084068, 0xD3000040, 0x1E644058, 0x1C49D1FA, 0x2A001E52, 0x4770D1F2,
    0xf3c04601, 0x28203007, 0x2204bf24, 0x1050eb02, 0x2810d205, 0x2203bf26, 0x1010eb02, 0xf4110880,
    0xbf181f80, 0x0010f040, 0x48714770, 0x6001496f, 0x60014970, 0x68014870, 0x01f0f041, 0x486f6001,
    0xf0106800, 0xd1080f20, 0xf245486d, 0x60015155, 0x60412106, 0x71fff640, 0x20006081, 0x49694770,
    0xf4206808, 0x600a52f8, 0x48676008, 0xf0416801, 0x60014100, 0x47702000, 0xc18cf8df, 0x0000f8dc,
    0x0004f040, 0x0000f8cc, 0x0000f8dc, 0x4000f440, 0x0000f8cc, 0x0000f8dc, 0x3080f440, 0x0000f8cc,
    0x0004f1ac, 0xf4116801, 0xbf1c3f80, 0x21aaf64a, 0xd0044a53, 0x68036011, 0x3f80f413, 0xf8dcd1fa,
    0xf0200000, 0xf8cc0004, 0xf8dc0000, 0xf4200000, 0xf8cc4000, 0x20000000, 0xf3c04770, 0x29203107,
    0x2204bf24, 0x1151eb02, 0x2910d205, 0x2203bf26, 0x1111eb02, 0xf4100889, 0xbf181f80, 0x0110f041,
    0x6802483d, 0x02f0f042, 0xf1006002, 0x22020c04, 0x2000f8cc, 0x2000f8dc, 0xea0323f8, 0x431101c1,
    0x1000f8cc, 0x1000f8dc, 0x3180f441, 0x1000f8cc, 0xf4116801, 0xbf1c3f80, 0x21aaf64a, 0xd0044a30,
    0x68036011, 0x3f80f413, 0xf8dcd1fa, 0xf0211000, 0xf8cc0102, 0x68011000, 0x0ff0f011, 0x2000bf04,
    0x68014770, 0x01f0f041, 0x20016001, 0x4b224770, 0x1cc9b430, 0xc000f8d3, 0x0103f031, 0x0cf0f04c,
    0xc000f8c3, 0x0404f103, 0x0c00f04f, 0xc000f8c4, 0xf240bf18, 0xd0252501, 0xc000f8d4, 0x0c05ea4c,
    0xc000f8c4, 0xc000f8d2, 0xc000f8c0, 0xc000f8d3, 0x3f80f41c, 0xf8d4d1fa, 0xf02cc000, 0xf8c40c01,
    0xf8d3c000, 0xf01cc000, 0xd0060ff0, 0xf0406818, 0x601800f0, 0x2001bc30, 0x1d004770, 0xf1021f09,
    0xd1d90204, 0x2000bc30, 0x00004770, 0x45670123, 0x40023c04, 0xcdef89ab, 0x40023c0c, 0x40023c14,
    0x40003000, 0x40023c00, 0x40023c10, 0x00000000
};

static const program_target_t flash = {
    0x2000004b+RAM_OFFSET, // Init
    0x2000007f+RAM_OFFSET, // UnInit
    0x20000099+RAM_OFFSET, // EraseChip
    0x200000fb+RAM_OFFSET, // EraseSector
    0x2000018f+RAM_OFFSET, // ProgramPage

    // BKPT : start of blob + 1
    // RSB  : blob start + header + rw data offset
    // RSP  : stack pointer
    {
        0x20000001+RAM_OFFSET,
        0x2000022c+RAM_OFFSET,
        0x20000000
    },

    0x20000000 + 0x00000A00+RAM_OFFSET,  // mem buffer location
    0x20000000+RAM_OFFSET,               // location to write prog_blob in target RAM
    sizeof(output_flash_prog_blob),   // prog_blob size
    output_flash_prog_blob,           // address of prog_blob
    0x00000400       // ram_to_flash_bytes_to_be_written
};
</code>

Pole ''output_flash_prog_blob[]'' je zkompilovaný kód, který musí být schopný běžet na cílovém procesoru (target). Lze jej vygenerovat z projektu FlashAlgo. Kód musí fungovat nezávisle na pozici v RAM (pouze relativní skoky aj.) a musí nutně implementovat následující fuknce:
  * inicializace flash (odemčení,...)
  * deinicializace flash
  * vymazání celé flash paměti
  * vymazání sektoru flash paměti
  * programování stránky flash paměti

Struktura ''program_target_t flash'' poskytuje zapisovacímu rozhraní:
  * informaci o tom, odkud v RAM se má jaká funkce spustit (inicializace, mazání, programování,...)
  * informaci o poloze breakpointu, délky, hlavičky,... a o poloze Stack Pointeru (u nás umístěná úplně na začátku tabulky vektorů)
  * adresu začátku bufferu
  * adresu, kam v RAM zapsat přeložený kód, jeho velikost, pointer na něj
  * kolik bajtů celkem zapsat
Oproti výstupu generovanému projektem FlashAlgo bylo nutné:
  * veškeré odkazy na RAM posunout o velikost tabulky vektorů (makro RAM_OFFSET)
  * ukazatel na Stack Pointer opravit (na začátek RAM, tabulky vektorů)

===== Změny v Daplink =====
Pro efektivní využití bylo navrženo upravit původní kód Daplink tak, aby:
  * bylo možné pomocí názvu souboru zvolit, zda bude při programování použita startovní adresa pro bootloader nebo firmware
  * bylo možné odlišit dvě stejná zařízení dle názvu
  * nedocházelo k mazání celé paměti před začátkem programování => sektorové mazání
  * sektorové mazání mazalo sektory různé velikosti

===== Hardwarová architektura =====
Hardwarová architektura vychází přímo z mbed HDK schématu pro LPC11U35 viz [[https://github.com/ARMmbed/mbed-HDK/tree/master/Production%20Design%20Projects/ARM-mbed/DAPLink/DIPDAP|DIPDAP]].

===== Použití programátoru =====
Programátor je velmi jednoduchý na použití. Připojením programátoru k PC jsou systémem registrována následující zařízení:
  * vyměnitelný disk s názvem ''BYZG3_****'' 
  * nový virtuální port
Přesunutím souboru *.bin nebo *.hex na vyměnitelný disk započne přenos souboru a jeho programování do cílového procesoru. Pokud je potřeba program nahrát do oblasti bootloaderu (tj. na začátek paměti), je třeba na flash disku vytvořit soubor s názvem ''BOOTLOAD.txt'' a poté započít přenos binárního souboru standartním způsobem. 

V případě, že nestane při nahrávání jakákoli chyba, je vyměnitelný disk odpojen a znovu připojen a v souboru FAIL.txt je chyba popsána.

V případě nutnosti nahrávat nový firmware pro programovací mikroprocesor je postup následující:
  * odpojit Daplink od napájení
  * podržet tlačítko ISP a připojit napájení
  * přihlásí se disk s názvem ''CRP DISABLD''; obsahuje jediný soubor firmware.bin, který je nutné smazat pro uvolnění místa
  * překopírováním nového *crc.bin souboru na disk je soubor nahrán do flash programovacího mikroprocesoru
  * restartováním je spuštěn Daplink s novým firmwarem

Programátor je dále možné ovládat pomocí MSD příkazů. Jejich zadávání spočívá v tom, že jsou na flashdisk nahrávány soubory s různými názvy. Ve výchozím nastavení jsou příkazy prováděny pouze pokud je současně stisknuto tlačítko ISP/RST (mód automation je vypnutý). Podrobnosti viz.: [[https://github.com/mbedmicro/DAPLink/blob/master/docs/MSD_COMMANDS.mdk|MSD Commands]].