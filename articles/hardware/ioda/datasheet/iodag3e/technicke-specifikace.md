# Technické specifikace zařízení IODAG3E 


## Mezní parametry 





## Doporučené opeační podmínky 





## Mechanické specifikace




## Technické specifikace

![Rozměry deska](/images/hardware/IODAG3E_170725_dimensions.png)
![Rozměry Konektory](/images/hardware/IODAG3E_170725_connectors.png)

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

