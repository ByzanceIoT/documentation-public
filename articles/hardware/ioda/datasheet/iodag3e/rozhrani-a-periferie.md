# Rozhraní a periférie

**Obsah:**

* [Blokové schéma](#block-diagram)
* [Metody napájení](#power) 
* [GPIO a sběrnice](#GPIO) 
* [Ethernet](#Ethernet)
* [WEXP module \(Lowpan\)](#WEXP)

## Blokové schéma {#block-diagram}

TO DO

## Metody napájení {#power}

Zařízení IODAG3E disponuje **třemi **standartními **napájecími vstupy** \(USB, PoE a napájení z externího zdroje\) s širokém rozsahem akceptovaného napájecího napětí. Všechny tři výše uvedené varianty mohou být bezpečně použity současně a lze je zapínat nezávisle na sobě.

Čtvrtou možností je použití signálu _**VBUS**_, který je vyveden na X a Y liště desky. Jeho použití **není **pro běžného uživatele **bezpečné **a není doporučené ho používat. Všechny možnosti jsou dále detailněji rozebrány.

**Příkon ** zařízení se v zásvislost na stavu, činnosti a zvoleném vstupu pohybuje od 0.6W do 0.9W \(Měřeno bez rozšiřujících desek a dalších připojených komponent\). Příkon je dále také ovlivněn amplitudou napájecího napětí. Všechny uváděné proudy jsou bezpečné proudy pro dlouhodobější provoz s ohledem na výkonové ztráty v systému \(zahřívání komponent\). Překročení **horní** hranice uvedených napětí může vést k **poškození **zařízení. Naopak **podpětí** a **nedostatečně dimenzovaný **vstup zdroje energie může zpusobit **nepředvídatelné chování **a nestabilitu.

Detailnější výsledky měření na napájecí kaskádě jsou dostupné v gitu \(rezpozitář _hardware/G3/IODAG3E/Measurements/22062017\_psu_\).

### USB

Zařízení se spustí neprodleně po připojení microUSB kabelu.

![MicroUSB](/images/hardware/microUSB.png)

Technické parametry USB vstupu:

* Doporučené vstupní napětí: 5.0V \(+-10% dle specifikací USB\)
* Doporučený maximální proud vstupem: 1.0A
* Vstup je vybaven přepěťovou ochranou: max. vstupní napětí je 6.0V

### PoE \(Power over Ethernet\)

Napájení po datovém síťovém kabelu, bez nutnosti přivést napájecí napětí k přístroji dalším samostatným kabelem. Rozlišuje se tzv. **aktivní **a **pasivní PoE**.

![MicroUSB](/images/hardware/POE.png)

#### Aktivní PoE

* Tato metoda je **Kompatibilní** se standartem **802.3af** \(802.3at Type 1, jedná se tedy o tzn. **aktivní** PoE\). Tento standart povoluje napětí od 37 do 57V, nicméně zařízení IODAG3E umožňuje  napájení přes PoE už od nižšího napětí \(Pasivní PoE\).

* IODA je _**Class 0**_ zařízení, tudíž přes PoE může odebírat max. 12.95W energie.

#### Pasivní PoE

* Zařízení akceptuje také **Pasivním PoE**, což znamená, že zařízení je možné napájet 6-60V na nevyužitých párech 100Mbit LAN kabelu.

K PoE se přistupuje podobným způsobem jako Mikrotic u zařízení \([http://www.wifihw.cz/img.asp?attid=22184](http://www.wifihw.cz/img.asp?attid=22184)\), kde se kombinují vlastnosti aktivního PoE s výhodami pasivního PoE pro dosažení maximální flexibility a jednoduchosti použití.

Technické vlastností PoE napájení:

* Rozsah vstupního napětí **6 - 60V AC/DC**
* Doporučený maximální proud vstupem: **0.5A**
* Vstup je vybaven přepěťovou ochranou dimenzovanou lehce nad **60V**

### Externí zdroj

Další metodou napájení je zapojení externího zdroje do zeleného konektoru na čelní straně desky vedle ethernetového kabelu. Výhodou je široký rozsah napájecího napětí a jeho nezávislost na polaritě.

![ext\_zdroj](/images/hardware/ext_zdroj.png)

Technické vlastností vstupu externího napájení:

* Rozsah vstupního napětí **6 - 60V AC/DC**
* Doporučený maximální proud vstupem: **0.5A**
* Vstup je vybaven přepěťovou ochranou dimenzovanou mírně nad **60V**

### VBUS

Jde o signál na liště X/Y, jehož **použití není** pro běžného uživatele **bezpečné **a a může vést ke zničení desky či připojeného zdroje. Na pin **VBUS** je možné aplikovat napětí přímo na **nechráněný** vstup spínanného zdroje a dosáhnout tak spuštění desky již od napětí typ. 4.0V.

Smyslem je umožnit běh desky z externího 5V zdroje \(typicky při vestavbě do existujícího 5V systému\). Tato věc je technicky možná, nicméně se silně **nedoporučuje** \(Spíše jen pro interní info\). Běžně **VBUS** slouží jako výstup pro napájení externích zařízení pomocí IODAG3E.

Technické vlastností napájení signálem VBUS:

* Rozsah vstupního napětí 4.0 - 60V DC \(horní limit maximální, doporučeno spíše 57V\)
* Doporučený maximální proud vstupem: 1.2A \(dáno šířkou spoje, 0.6mm/18um\)
* Pro použití nutno vodivě spojit pájecí propojku SJ1 \(vedle tlačítka RST\)

## GPIO a sběrnice {#GPIO}

Zařízení IODA dispouje sběrnicí GPIO s celkem 54 piny. Na GPIO lze definovat digitální i analogové vstupy a výstupy a další komunikační rozhraní

### Pinout

Sběrnice GPIO je rozdělena na dvě části a to **X-Konektor** a **Y-Konektor**

#### X-Konektor

#### Y-konektor


### Analogové výstupy

### Analogové vstupy

### I2C

Zařízení IODA má na GPIO sběrnici k dispozici dvě sběrnice I2C. Obě sběrnice nabízejí možnost využití alternativního zapojení na jiné dvojici pinů.

| **Funkce ** | **Pin** | **Alternativní pin** |
| :--- | :--- | :--- |
| **I2C1 SCL** | **X06** | **X15** |
| **I2C1 SDA** | **X07** | **X13** |
| **I2C3 SCL** | **Y07** | **Y21** |
| **I2C3 SDA** | **Y06** | **Y20** |

### UART/USART

IODA umožňuje komunikovat po několika sériových linkách. Na jeho sběrnici GPIO lze definovat až 4x komunikační rozhraní typu **UART** a jedno komunikační rozhraní **USART**





### SPI

### CAN

## Ethernet {#Ethernet}

## WEXP module \(Lowpan\) {#WEXP}



