# IODAG3E

Technická specifikace

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

### Napájení

První tři varianty \(USB, PoE, externí zdroj\) napájení mohou být použity současně a je to bezpečné \(z pohodlnosti, jako záloha, ..\). Použití možnosti \*\*MAIN\_PWR\_OUT\*\* vylučuje použít současně jakýkoliv jiný zdroj.

#### USB

```
\* klasika, 5V, doporučený max. proud 1000mA 

\* Dle tolerancí USB je napětí +-10% a deska to splňuje a je ochotná startovat od 4,5V na USB.
```

#### PoE

Napájení přes LAN kabel

* Kompatibilita se \*\*standartem 802.3af\*\* \(802.3at Type 1\). Nelze říct, že \*\*podpora\*\* standartu 802.3af, protože PoE uvedeného standartu povoluje napětí od 37 do 57V. My chceme jít od nižšího napětí a proto jsme jen kompatibilní a navíc umíme i níže uvedené pasivní PoE.
* IODA je navržen jako //Class 0// zařízení z čehož vyplívá, že přes PoE může odebírat max. 12.95W energie.
* Zároven umíme tzv. \*\*pasivní PoE\*\*. Tzn. akceptujeme napájecí napětí 10 - 60V na nevyužitých párech 100Mbit LAN kabelu \(10V spodní hranice je otázkou domluvy, technicky je limit cca 6,5V\). Doporučený max. proud vstupem 500mA.
* Víceméně k PoE přistupujeme jako Mikrotik na jejich zařízeních \(\[\[[http://www.wifihw.cz/img.asp?attid=22184\|ukázka](http://www.wifihw.cz/img.asp?attid=22184|ukázka) popisku\]\]\).

#### Externí zdroj

```
  \* AC/DC, napětí 10-60V, proud až 500mA \(technicky stejně jako u pasivního PoE\)

  \* Je to ten zelený konektor vedle ethernetového kabelu. Polarita napětí není podstatná.
```

#### MAIN\_PWR\_OUT

signál na liště X/Y

* na daný signál je možné aplikovat \*\*nechráněné napětí\*\* přímo na vstup spínanného zdroje a dosáhnout tak běhu YODY v rozmezí 4-57V. Maximální proud vstupem 1200mA \(dáno šířkou spoje, 0.6mm/18um\).
* Umožnuje běh YODY z externího 5V zdroje \(typicky při vestavbě do existujícího 5V systému\). 
* Tato věc je technicka možná, nicméně se silně nedoporučuje. \*\*Člověk musí chápat, co dělá.\*\* Spíš jen pro interní info.

Všechny uvedené proudy jsou bezpečné proudy pro dlouhodobější provoz s ohledem na výkonové ztráty v systému \(zahřívání komponent\). Překročení \*\*horní\*\* hranice uvedených \*\*napětí\*\* může vést k \*\*poškození\*\* zařízení. Naopak \*\*podpětí\*\* a \*\*nedostatečně dimenzovaný\*\* vstup zdroj energie může zpusobit \*\*nepředvídatelné chování\*\*.

Detailnější výsledky měření na napájecí kaskádě jsou dostupné v gitu \(//hardware/IODAG3/Measurements/22062017\_psu//\).

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

