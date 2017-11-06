# IODAG3E

* todo: pár vět/odstavců s krátkým a stručným přehledem, co tato deska je, k čemu slouží a co umí a asi fotku, další detaily bych dal do podkapitol

### Mikrokontrolér 
* STM32F437IIH6 \([Datasheet](http://www.st.com/content/ccc/resource/technical/document/datasheet/fd/8c/0a/19/13/8f/41/99/DM00077036.pdf/files/DM00077036.pdf/jcr:content/translations/en.DM00077036.pdf)\)
* 2 MB Flash
* 192 kB SRAM \(včetně 64 KB CCM\)
* Programování pomocí SWD
* Periferie I2C, U\(S\)ART, SPI, CAN, SAI, USB2.0, Ethernet, Crypto hardware akcelerace, CRC jednotka

### Ethernet

* Budič LAN8720 \([Datasheet](http://ww1.microchip.com/downloads/en/DeviceDoc/8720a.pdf)\)
* Podpora PoE 
* Rychlost do 100Mbit

### LowPAN

viz \[\[lowpan:teoreticke\_informace\_lowpan\|Základní teoretické informace o použité technologii LoWPAN\]\] \(ticket HW-632\)

* 868 MHz

* přenosová rychlost až 10 kBps

* možnost režimu border router \(sdílení Internetového připojení pro LowPAN síť - NAT64, DNS64\) viz. \[\[feature:lowpanbr\|Lowpan BR\]\]

* možnost připojení k Internetu prostřednictvím LowPAN sítě viz. \[\[feature:lowpan\|6Lowpan\]\]

### Externí paměť

* 8MB \(64Mb\) externí flash paměť \(\[\[tutorial:nonvolatile\| dokumentace\]\]\) 

### Uživatel

* Tlačítko pro RESET
* Tlačítko USER
* RGB LED pro signalizaci

## Napájení 

Zařízení IODAG3E disponuje **třemi **standartními **napájecími vstupy** \(USB, PoE a napájení z externího zdroje\) s širokém rozsahem akceptovaného napájecího napětí. Všechny tři výše uvedené varianty mohou být bezpečně použity současně a lze je zapínat nezávisle na sobě. 

Čtvrtou možností je použití signálu _**VBUS**_, který je vyveden na X a Y liště desky. Jeho použití **není **pro běžného uživatele **bezpečné **a není doporučené ho používat. Všechny možnosti jsou dále detailněji rozebrány.

**Příkon ** zařízení se v zásvislost na stavu, činnosti a zvoleném vstupu pohybuje od 0.6W do 0.9W (Měřeno bez rozšiřujících desek a dalších připojených komponentech). Příkon je dále také ovlivněn amplitudou napájecího napětí. Všechny uváděné proudy jsou bezpečné proudy pro dlouhodobější provoz s ohledem na výkonové ztráty v systému \(zahřívání komponent\). Překročení **horní** hranice uvedených napětí může vést k **poškození **zařízení. Naopak **podpětí** a **nedostatečně dimenzovaný **vstup zdroj energie může zpusobit **nepředvídatelné chování **a nestabilitu.

Detailnější výsledky měření na napájecí kaskádě jsou dostupné v gitu \(rezpozitář _hardware/G3/IODAG3E/Measurements/22062017\_psu_\).

### USB

Zařízení se spustí neprodleně po připojení microUSB kabelu.

Technické parametry USB vstupu:

* doporučené vstupní napětí: 5.0V \(+-10% dle specifikací USB\)
* doporučený maximální proud vstupem: 1.0A
* vstup je vybaven přepěťovou ochranou: max. vstupní napětí je 6.0V

### PoE

Napájení po datovém síťovém kabelu, bez nutnosti přivést napájecí napětí k přístroji dalším samostatným kabelem. Rozlišuje se tzv. **aktivní **a **pasivní PoE**.

#### **Aktivní PoE **

* **Kompatibilita **se standartem **802.3af** \(802.3at Type 1, tzn. **aktivní** PoE\). Nelze doslovně uvést **podporujeme** standart 802.3af, protože PoE uvedeného standartu povoluje napětí od 37 do 57V. My chceme jít od nižšího napětí a proto jsme **jen** **kompatibilní **s daným standartem a navíc umíme i níže uvedené pasivní PoE, které funguje od nižšího napětí.
* IODA je _**Class 0**_ zařízení, tudíž přes PoE může odebírat max. 12.95W energie.

#### P**asivní PoE **

* Zároven umíme tzv. **pasivní **PoE. Tzn. akceptujeme napájecí napětí 6 - 60V na nevyužitých párech 100Mbit LAN kabelu. 

Víceméně k PoE přistupujeme jako Mikrotik na jejich zařízeních \([http://www.wifihw.cz/img.asp?attid=22184](http://www.wifihw.cz/img.asp?attid=22184|ukázka)\). Kombinují se vlastnosti aktivního PoE s výhodami pasivního PoE pro dosažení maximální flexibility a jednoduchosti použití \(tj. funguje to jednoduše a za všech okolností\). 

Technické vlastností PoE napájení:

* rozsah vstupního napětí 6 - 60V AC/DC
* doporučený maximální proud vstupem: 0.5A
* vstup je vybaven přepěťovou ochranou zasahující lehce nad 60V

### Externí zdroj

 Jde o napájení přivedené do zeleného konektoru na čelní straně desky vedle ethernetového kabelu. Výhodou je široký rozsah napájecího napětí a jeho nezávislost na polaritě.

Technické vlastností vstupu externího napájení:

* rozsah vstupního napětí 6 - 60V AC/DC
* doporučený maximální proud vstupem: 0.5A
* vstup je vybaven přepěťovou ochranou zasahující lehce nad 60V

### VBUS

Jde o signál na liště X/Y, jehož** použití není **pro běžného uživatele **bezpečné **a a může vést ke zničení desky či připojeného zdroje. Na daný signál je možné aplikovat napětí přímo na **nechráněný** vstup spínanného zdroje a dosáhnout tak běhu desky již od napětí typ. 4.0V.

Smyslem je umožnit běh desky z externího 5V zdroje \(typicky při vestavbě do existujícího 5V systému\). Tato věc je technicky možná, nicméně se silně **nedoporučuje**. Člověk musí chápat, co dělá. Spíš jen pro interní info. 

Technické vlastností napájení signálem VBUS:

* rozsah vstupního napětí 4.0 - 60V DC \(horní limit maximální, doporučeno spíše 57V\)
* doporučený maximální proud vstupem: 1.2A \(dáno šířkou spoje, 0.6mm/18um\)
* pro použití nutno vodivě spojit pájecí propojku SJ1 \(vedle tlačítka RST\)



### Rozměry a hmotnost

\* rozměry samotného PCB jsou 41x63mm

\* rozměry včetně přečnívajícího RJ45, napájecího a USB konektoru jsou 42,5x65,5mm

\* celková výška včetně konektorů 11,5mm, výška od horní strany PCB 8,5mm

\* váha 60g \(hrubý odhad\)

\* rozměrové náčrtky:

```
\* Rozměry: {{:specs:iodag3e\_250717\_dimensions.png?linkonly\|PNG}}, {{:specs:iodag3e\_250717\_dimensions.pdf\|PDF}}, DXF: naše wiki nedovolí upload, je to v gitu

\* Konektory: {{:specs:iodag3e\_250717\_connectors.png?linkonly\|PNG}}{{:specs:iodag3e\_250717\_connectors.pdf\|PDF}}, DXF: naše wiki nedovolí upload, je to v gitu
```

### Software

Programování je možné z online IDE Byzance FIXME doplnit, nebo \[\[tutorial:programming\|lokálně pomocí programátoru\]\].

Vývoj je možný v \[\[[http://www.cplusplus.com/reference/\|C/C++\]\](http://www.cplusplus.com/reference/|C/C++]\)\], dále je možné využívat API \[\[tutorial:mbed\|MBED\]\], a pro připojení k Byzance serverům a Blocku jsou implementovány speciální \[\[tutorial:byzance\_io\|Byzance vstupy a výstupy\]\]. Základní operace,

spojení k serverům a údržbu desky zajišťují \[\[tutorial:public\_functions\|veřejné metody\]\] třídy Byzance.

==== Netechnické marketing řeči ====

== Hardware ==

\* na to jak je to kompaktní, to umí dost věcí a není to výkonově slabé

\* je to postavené na kvalitních součástkách \(není to ultra lowcost a tomu kvalita odpovídá\)

\* vybavené ochranami na datových rozhraních \(USB, ETH\) a napájení \(chráněná napájení všechna, kromě \*\*MAIN\_PWR\_OUT\*\*\)

\* použitá bezdrátová technologie \(\[\[lowpan:teoreticke\_informace\_lowpan\|6LoWPAN\]\]\) je fakt dobrá a umí dost věcí a podporujeme přímou adresaci prvku přes IPv6

\* disponuje efektivním spínaným zdrojem s širokým rozsahem vstupního napájení

\* velké množství vstupně výstupních pinů pro snadné připojení externím komponent \(včetně napájecích a řídicích signálů\)

```
\* \*\*X sběrnice/konektor:\*\* určený zejména pro připojování rozšiřujících shieldů; standartní dutinková lišta 2x10 s roztečí 2.54mm

\* \*\*Y sběrnice/konektor:\*\* další vstupně výstupní piny; podoba půlených frézovaných prokovů s roztečí 1.27mm

\* \*\*expanzní konektor:\*\* primárně/aktuálně určený pro modul bezdrátové technologie \[\[lowpan:teoreticke\_informace\_lowpan\|6LoWPAN\]\], obsahuje však i další signály a lze použít i na jiné účely \(např. SD karta, rozhraní drátové sběrnice, ...\)
```

\* LED diody a tlačítka:

```
\* RGB LED pro signalizaci stavů systému s možností plně uživatelského řízení pro vlastní účely

\* zelená //power LED// signalizuje správnou funkci spínanného zdroje

\* zelená/oranžová LED stavy ethernetu \(náhrada za LED, co jsou obyčejně v LAN konektoru\)

\* deska disponuje tlačítem \(//reset button/rst btn//\) pro reset systému a uživatelským tlačítkem \(//user button/usr btn//\)
```

\* široké možnosti vestavby do zařízení

```
\* celé zařízení je možné připájet na vlastní PCB

\* montáž na distanční sloupky 

\* provoz zcela samostatně
```

\* každé zařízení má své unikátní ID a svou unikátní MAC adresu

== Firmware==

\* vestavěný webový server využívaný pro debugovací a statistické údaje

\* automatické zálohování a obnova firmware při jeho selhání

\* podpora vzdálené aktualizace firmware //Update over the air// \(také možnost použít SWD rozhraní a nebo //drag & drop// přes USB\)

\* díky \[\[lowpan:teoreticke\_informace\_lowpan\|6LoWPAN\]\] modulu možnost:

```
\* budovat větší sítě s prvky ne přímo připojenými do internetu

\* MESH sítí s jejími benefity \(rozšíření dosahu bezdrátovo signálu, přizpusobení přenosové cesty za běhu, větší odolnost proti výpadkům\)
```

\* dohled nad během firmware přes interní watchdog

