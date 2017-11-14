# Beginner's Guide

Vítej ještì jednou v Byzance. Zde je seznam, co vše bìhem úvodního tutoriálu probereme.

## List of Steps

1. [Vlastní úèet](#own-account)
2. [Vlastní Tariff](#own-tariff)
3. [První Projekt](#first-project)
   1. Základní pøehled
   2. Vysvìtlení Menu
4. [Registrace Hardwaru](#registrace-hardwaru)
5. První program pro Hardware
6. Nahrátí programu na Hardware
7. První Blocko
8. První Vlastní Bloèek
9. Integrace Blocko s Hardwarem
10. První vlastní Instance
11. První Aplikace v Gridu 
12. První vlastní Widget
13. Integrace s Blocko

---

### Vlastní úèet {#own-account}

První vìc, kterou musíš udìlat je vytvoøit si úèet úèet na Portálu Byzance \([portal.byzance.cz](/portal.byzance.cz)\)

V pøihlašovacím oknì se lze pøilásit s vyuitím úètu Facebook èi Github nebo se registrovat vytvoøením nového Byzance úètu kliknutím na tlaèítko **Create an account**. Pøi registraci nového byzance úètu je nutné vyplnit poadované údaje a vyèkat na potvrzovací email, kterı bude zaslán na zadanou adresu.

Po úspìšném pøihlášení se zobrazí Dashboard portálu Byzance.

#### **Co je Portál**

Portál je internetová aplikace vytvoøená Byzance, která slouí jako brána pro všechna Byzance IoT zaøízení ke komunikaci s okolním svìtem. Portál zároveò uivateli slouí jako prostøedí, ve kterém vytváøí funkèní kód, uploaduje tento kód do síì svıch zaøízení a dochází k aktualizaci zaøízení. Dokumentace, krok po kroku vysvìtluje, jak provést základní konfiguraci.

---

### Vlastní Tariff {#own-tariff}

V levém Menu Najdi odkaz Financial \([portal.byzance.cz/financial](/portal.byzance.cz/financial)\)  
Vytvoø si novı úèet a vyber si - kterı typ úètu ti nejvíce vyhovuje. **I do it for my self** or **I will be integrator**. Na stránce máš více rozepsané, co k èemu slouí.

#### **Co jsou to Tarify **

Jeliko jsou nìkteré naše sluby placené a protoe chceme umonit i velkım firmám pracovat a spravovat své produkty ve sloité hierarchii, jsou všechny aktivity vázané na Tariffs. Tarify jsou Úèetní entity, která má vlasntíka \(neboli správce\) v podobì fyzické osoby \(zakladatel úètu\) nebo firmy \(lze nastavit\) a také fakturované jednotky buï jde o stejnou osobu / firmu - nebo externí firmu. Lze tedy Vytvoøit i Tarrif, kterého jsem vlastník - ale fakturuje se to tøetí osobì. Tento model je vhodnı pro Freelancery nebo Integrátory. Integrátor tak mùe vytváøet zakázkové projekty pro desítky svıch klientù a mít tak dokonalı pøehled o celkovıch nákladech kadého klienta. Tariff lze migrovat i na jiné úèty a firmy. Takto lze vytváøet rùzné kombinace desítek finanèních entit.

#### ** Jakı je rozdíl v tariffech? **

Rozdíl není ádnı - jde jen o poèáteèní stav. To s èím na zaèátku zaèínáš.  Kadı Tariff se skládá z Extensions \(Extensions pro vyšší poèet HW, Extensions Pro vyšší objem pøenesenıch dat atd.\). Take na zaèátku máš nìkteré Tariffy, které u mají pøedplacenı vyšší objem dat, nebo vyšší poèet uivatelù, kteøí se mohou spravovat projekty. Naše zkušenosti nám øíkají, e nìkteøí zákazníci mají rádi u od zaèátku vše aktivní a tak jsme jim pøipravili ji pøedkonfigurované Tariffy obsahující dùleité funkce. Pokud si nevíš rady, prostì zaèni s tím základním a postupnì si pøidávej jednotlivé funkce. Nìkteré tariffy u od zaèátku vyadují plnohodnotnou registraci vèetnì emergency kontaktù a dalších. Tyto kontakty NIKDY NESLOUÍ K MARKETINGU! Ale jsou pouity vıluènì pro technickou a bezpeèností podporu. \(Naše servisní støedisko vás mùe v nìkterıch pøípadech kontaktovat pokud dojde k vánım incidentùm\)

#### ** Co jsou Extensions? **

Extensions jsou balíèky, je lze kdykoliv nebo i na zaèátku pøikupovat do svého Tariffu. Na zaèátku kadı tariff obsahuje základní sadu balíèkù. Díky nim se nám snadno zpøístupòují jendnotlivé funkce pro naše zákazníky. Nìkteré jsou zdarma, jiné ve zpoplatnìnıch tariffech u mìsíènì nìco stojí. Vìtšina Extensions je zaloena na poplatcích na mìsíèní bázy. Nìkteré poskytuje pøímo Byzance, jiné jsou tøetích stran. Balíèky mají vlastní konfiguraci - zaloené na tom, co kterı balíèek umonuje. Napøíklad potøebuješ-li databázi k uskladnìní svıch dat, lze aktivovat balíèek "Databáze" s rùznou velikostí podle potøeb s rùznou cenou. U nìkterıch je aktivní sleva z rozsahu.

---

### První Projekt {#first-project}

Teï tì èeká vytvoøení tvého prvního projektu. Kadı projekt je vázanı na nìkterı z tvıch finanèních produktù \(Tariffech\). Pokud ho nemáš - vra se k bodu èíslo 2. **Tadááá - Máš svùj první projekt. Gratulujeme! &lt;3 **

#### **Overview:**

* **DashBoard**: je vıchozí obrazovka projektu, kde máš základní pøehled všeho.

* **Members**: Je správce úètù, které mohou s projektem manipulovat. Lze nastavit práva tak jak jednotlivım uivatelùm dùvìøuješ. Mùeš pozvat své kolegy, kteøí u úèet mají, nebo si ho díky pozvánce teprve vytvoøí. Pozvaní nemusejí ji vytváøet vlastní finanèní produkty a ani do nich nemají pøístup. \(Jen pokud by si je jmenoval i správcem Financial Tariff.\)

* **HARDWARE**: Je Stránka, která ti zobrazuje tvùj zaregistrovanı Hardware a jeho manaerské nástroje. Na kadé stránce, která obsahuje seznam v tabulce \(všude v portálu\) lze vykreslit maximálnì 25 prvkù. Pro zobrazení dalších prvkù, pouívej šipky nebo parametry filtru.

  * **Hardware list**: Seznam tvého Hardwaru. Jako ho zaregistrovat se dozvíš níe.

  * **Hardware Groups**: Ti umoní vytváøet skupiny Hardwaru, které jsou si nìèím podobné nebo ti umoní speciální dìlení. Napøíklad "German Market", "Generation v1.3", "Office Flor 3". Díky skupinám mùeš vyuívat nástroje hromadného updatu.

  * **Updates**: Je seznam všech tvıch updatù, jednotlivıch individuálních i tìch hromadnıch. Na této stránce díky tlaèítku "Release Firmware" mùeš aktualizovat skupinu, kde lze vybrat Program a jeho verzi, nebo Bootloader. Aktualizaèní proceduru lze i naplánovat na èas, kterı ti vyhovuje.

* **CODE**: Je první Cloud Tool v našem Portálu, kterı ti umonuje jednoduše programovat Hardware.

  * **Code Programs**:: Obsahuje dvì sekce. Tvé vlastní programy a programy vytvoøené Byzance, komunitou nebo jednotlivımi dodavately Hardwaru. Veøejné programy si mùeš zkopírovat a dále upravovat. Nezapomeò, e i ty mùeš jednotlivé programy v platformì sdílet s ostatními. Sdílení je jen kontrolováno administrátory.

  * **Code Libraries**:: Knihovny jsou pøedpøipravené balíèky kodu, je ti umoní velmi snadno integrovat speciální funkce nebo obsluhu Shieldu pro tvùj Hardware.

* **GRID**: Je nástroj pro tvorbu jednoduchıch ovládacích aplikací pøímo na míru k jendomu HW nebo celé skupinì. Grid nemá za cíl udìlat dokonalé sexy vypadající aplikace pro vaše zákazníky - doporuèujeme dìlat nativní s podporou Rest-Api, ale umonit ti tvoøit jednoduché øídící aplikace pro prùmysl a prùmyslové øízení s prezentací dat.

  * **Grid Apps**::
  * **Grid Widgets**::

  Grid se skládá s kolekce aplikací - a s Widgetù

* BLOCKO: TODO

* CLOUD:  TODO

---

### Registrace Hardwaru





---

### První program pro Hardware



---

### Nahrátí programu na Hardware



---

### První Blocko Program





První Vlastní Bloèek

Integrace Blocko s Hardwarem

První vlastní Instance

První Aplikace v Gridu

První vlastní Widget

Integrace s Blocko

#### 

#### Konfigurace hardware

Následující dokumentace pomáhá uivateli pøi prvním spuštìní a základní konfiguraci novì zakoupenıch zaøízení. Bliší informace a specifikace jednotlivıch zaøízení lze nalézt v [Hardwarové dokumentaci](Odkaz na Hardwarovou docu). Bìhem konigurace lze indentifikovat chování zaøízení pomocí LED signalizace, kterou zaøízení provádí. Vıznam tìchto LED signálù, lze vyhledat v Hardvarové dokumentaci jednotlivıch typù zaøízení v sekci [LED signalizace](/byzance_documentation/hardware_intro/hardware/iodag3e/led-signalizace.md)

