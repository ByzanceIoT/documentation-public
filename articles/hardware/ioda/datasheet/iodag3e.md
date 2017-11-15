# IODAG3E

IODAG3E je platforma sloužící pro přímou implementaci funkčního uživatelského programu a zároveň funguje jako IoT Gateway přímo komunikující s Cloudem skrze ethernetové rozhraní. Výsadou tohoto zařízení je velké množství výstupních a vstupních periférií, které umožňují vysokou variabilitu využití jak v průmyslu, tak domácí automatizaci či menších aplikacích.


## Mikroprocesor 

* STM32F437IIH6 \([Datasheet](http://www.st.com/content/ccc/resource/technical/document/datasheet/fd/8c/0a/19/13/8f/41/99/DM00077036.pdf/files/DM00077036.pdf/jcr:content/translations/en.DM00077036.pdf)\)
* 2 MB Flash
* 180 MHz
* 192 kB SRAM \(včetně 64 KB CCM\)
* Programování pomocí SWD
* MAC adresa

## Periférie 

* Etherent
* Lowpan
* GPIO Header (41 pinů) 
* A/D, D/A převodníky
* SPI 
* CAN
* UART
* I2C
* SAI
* USB 2.0

## Další funkce

* Integrované komunikační rozhraní s portálem
* Vzdálená aktualizace uživatelského programu
* Vestavěný webový server
* Konektor na uchycení Lowpan modulu WEXP pro bezdrátovou komunikaci
* Low power manegment
* CRC výpočetní jednotka
* Cryptografická hardwarová akcelerace
* watchdog
* Automatické zálohování uživatelského programu a jeho obnova při selhání
* Možnost vestavění na vlastní PCB


## Možnosti napájení 

Zařízení disponuje efektivním spínaným zdrojem s širokým rozsahem vstupního napětí.

Lze napájet přes:

* MicroUSB 
* Externí zdroj 6-60V AC/DC
* POE (aktivní/pasivní)
* Napájení z baterie

## Tlačítka 

* Tlačítko pro RESET
* Tlačítko USER

## Led signalizace 

* RGB LED modul

## Rozměry a hmotnost
  
 * Rozměry desky včetně konektorů : 42,5 x 65,5 mm
 * Výška včetně konektorů: 11.5 mm
 * Hmotnost: 60g

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

