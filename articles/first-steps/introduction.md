# Beginner's Guide

V�tej je�t� jednou v Byzance. Zde je seznam, co v�e b�hem �vodn�ho tutori�lu probereme.

## List of Steps

1. [Vlastn� ��et](#own-account)
2. [Vlastn� Tariff](#own-tariff)
3. [Prvn� Projekt](#first-project)
   1. Z�kladn� p�ehled
   2. Vysv�tlen� Menu
4. [Registrace Hardwaru](#registrace-hardwaru)
5. Prvn� program pro Hardware
6. Nahr�t� programu na Hardware
7. Prvn� Blocko
8. Prvn� Vlastn� Blo�ek
9. Integrace Blocko s Hardwarem
10. Prvn� vlastn� Instance
11. Prvn� Aplikace v Gridu 
12. Prvn� vlastn� Widget
13. Integrace s Blocko

---

### Vlastn� ��et {#own-account}

Prvn� v�c, kterou mus� ud�lat je vytvo�it si ��et ��et na Port�lu Byzance \([portal.byzance.cz](/portal.byzance.cz)\)

V p�ihla�ovac�m okn� se lze p�il�sit s vyu�it�m ��tu Facebook �i Github nebo se registrovat vytvo�en�m nov�ho Byzance ��tu kliknut�m na tla��tko **Create an account**. P�i registraci nov�ho byzance ��tu je nutn� vyplnit po�adovan� �daje a vy�kat na potvrzovac� email, kter� bude zasl�n na zadanou adresu.

Po �sp�n�m p�ihl�en� se zobraz� Dashboard port�lu Byzance.

#### **Co je Port�l**

Port�l je internetov� aplikace vytvo�en� Byzance, kter� slou�� jako br�na pro v�echna Byzance IoT za��zen� ke komunikaci s okoln�m sv�tem. Port�l z�rove� u�ivateli slou�� jako prost�ed�, ve kter�m vytv��� funk�n� k�d, uploaduje tento k�d do s�� sv�ch za��zen� a doch�z� k aktualizaci za��zen�. Dokumentace, krok po kroku vysv�tluje, jak prov�st z�kladn� konfiguraci.

---

### Vlastn� Tariff {#own-tariff}

V lev�m Menu Najdi odkaz Financial \([portal.byzance.cz/financial](/portal.byzance.cz/financial)\)  
Vytvo� si nov� ��et a vyber si - kter� typ ��tu ti nejv�ce vyhovuje. **I do it for my self** or **I will be integrator**. Na str�nce m� v�ce rozepsan�, co k �emu slou��.

#### **Co jsou to Tarify **

Jeliko� jsou n�kter� na�e slu�by placen� a proto�e chceme umo�nit i velk�m firm�m pracovat a spravovat sv� produkty ve slo�it� hierarchii, jsou v�echny aktivity v�zan� na Tariffs. Tarify jsou ��etn� entity, kter� m� vlasnt�ka \(neboli spr�vce\) v podob� fyzick� osoby \(zakladatel ��tu\) nebo firmy \(lze nastavit\) a tak� fakturovan� jednotky bu� jde o stejnou osobu / firmu - nebo extern� firmu. Lze tedy Vytvo�it i Tarrif, kter�ho jsem vlastn�k - ale fakturuje se to t�et� osob�. Tento model je vhodn� pro Freelancery nebo Integr�tory. Integr�tor tak m��e vytv��et zak�zkov� projekty pro des�tky sv�ch klient� a m�t tak dokonal� p�ehled o celkov�ch n�kladech ka�d�ho klienta. Tariff lze migrovat i na jin� ��ty a firmy. Takto lze vytv��et r�zn� kombinace des�tek finan�n�ch entit.

#### ** Jak� je rozd�l v tariffech? **

Rozd�l nen� ��dn� - jde jen o po��te�n� stav. To s ��m na za��tku za��n�.  Ka�d� Tariff se skl�d� z Extensions \(Extensions pro vy��� po�et HW, Extensions Pro vy��� objem p�enesen�ch dat atd.\). Tak�e na za��tku m� n�kter� Tariffy, kter� u� maj� p�edplacen� vy��� objem dat, nebo vy��� po�et u�ivatel�, kte�� se mohou spravovat projekty. Na�e zku�enosti n�m ��kaj�, �e n�kte�� z�kazn�ci maj� r�di u� od za��tku v�e aktivn� a tak jsme jim p�ipravili ji� p�edkonfigurovan� Tariffy obsahuj�c� d�le�it� funkce. Pokud si nev� rady, prost� za�ni s t�m z�kladn�m a postupn� si p�id�vej jednotliv� funkce. N�kter� tariffy u� od za��tku vy�aduj� plnohodnotnou registraci v�etn� emergency kontakt� a dal��ch. Tyto kontakty NIKDY NESLOU�� K MARKETINGU! Ale jsou pou�ity v�lu�n� pro technickou a bezpe�nost� podporu. \(Na�e servisn� st�edisko v�s m��e v n�kter�ch p��padech kontaktovat pokud dojde k v�n�m incident�m\)

#### ** Co jsou Extensions? **

Extensions jsou bal��ky, je� lze kdykoliv nebo i na za��tku p�ikupovat do sv�ho Tariffu. Na za��tku ka�d� tariff obsahuje z�kladn� sadu bal��k�. D�ky nim se n�m snadno zp��stup�uj� jendnotliv� funkce pro na�e z�kazn�ky. N�kter� jsou zdarma, jin� ve zpoplatn�n�ch tariffech u� m�s��n� n�co stoj�. V�t�ina Extensions je zalo�ena na poplatc�ch na m�s��n� b�zy. N�kter� poskytuje p��mo Byzance, jin� jsou t�et�ch stran. Bal��ky maj� vlastn� konfiguraci - zalo�en� na tom, co kter� bal��ek umo�nuje. Nap��klad pot�ebuje�-li datab�zi k uskladn�n� sv�ch dat, lze aktivovat bal��ek "Datab�ze" s r�znou velikost� podle pot�eb s r�znou cenou. U n�kter�ch je aktivn� sleva z rozsahu.

---

### Prvn� Projekt {#first-project}

Te� t� �ek� vytvo�en� tv�ho prvn�ho projektu. Ka�d� projekt je v�zan� na n�kter� z tv�ch finan�n�ch produkt� \(Tariffech\). Pokud ho nem� - vra� se k bodu ��slo 2. **Tad��� - M� sv�j prvn� projekt. Gratulujeme! &lt;3 **

#### **Overview:**

* **DashBoard**: je v�choz� obrazovka projektu, kde m� z�kladn� p�ehled v�eho.

* **Members**: Je spr�vce ��t�, kter� mohou s projektem manipulovat. Lze nastavit pr�va tak jak jednotliv�m u�ivatel�m d�v��uje�. M��e� pozvat sv� kolegy, kte�� u� ��et maj�, nebo si ho d�ky pozv�nce teprve vytvo��. Pozvan� nemusej� ji� vytv��et vlastn� finan�n� produkty a ani do nich nemaj� p��stup. \(Jen pokud by si je jmenoval i spr�vcem Financial Tariff.\)

* **HARDWARE**: Je Str�nka, kter� ti zobrazuje tv�j zaregistrovan� Hardware a jeho mana�ersk� n�stroje. Na ka�d� str�nce, kter� obsahuje seznam v tabulce \(v�ude v port�lu\) lze vykreslit maxim�ln� 25 prvk�. Pro zobrazen� dal��ch prvk�, pou��vej �ipky nebo parametry filtru.

  * **Hardware list**: Seznam tv�ho Hardwaru. Jako ho zaregistrovat se dozv� n�e.

  * **Hardware Groups**: Ti umo�n� vytv��et skupiny Hardwaru, kter� jsou si n���m podobn� nebo ti umo�n� speci�ln� d�len�. Nap��klad "German Market", "Generation v1.3", "Office Flor 3". D�ky skupin�m m��e� vyu��vat n�stroje hromadn�ho updatu.

  * **Updates**: Je seznam v�ech tv�ch updat�, jednotliv�ch individu�ln�ch i t�ch hromadn�ch. Na t�to str�nce d�ky tla��tku "Release Firmware" m��e� aktualizovat skupinu, kde lze vybrat Program a jeho verzi, nebo Bootloader. Aktualiza�n� proceduru lze i napl�novat na �as, kter� ti vyhovuje.

* **CODE**: Je prvn� Cloud Tool v na�em Port�lu, kter� ti umo�nuje jednodu�e programovat Hardware.

  * **Code Programs**:: Obsahuje dv� sekce. Tv� vlastn� programy a programy vytvo�en� Byzance, komunitou nebo jednotliv�mi dodavately Hardwaru. Ve�ejn� programy si m��e� zkop�rovat a d�le upravovat. Nezapome�, �e i ty m��e� jednotliv� programy v platform� sd�let s ostatn�mi. Sd�len� je jen kontrolov�no administr�tory.

  * **Code Libraries**:: Knihovny jsou p�edp�ipraven� bal��ky kodu, je� ti umo�n� velmi snadno integrovat speci�ln� funkce nebo obsluhu Shieldu pro tv�j Hardware.

* **GRID**: Je n�stroj pro tvorbu jednoduch�ch ovl�dac�ch aplikac� p��mo na m�ru k jendomu HW nebo cel� skupin�. Grid nem� za c�l ud�lat dokonal� sexy vypadaj�c� aplikace pro va�e z�kazn�ky - doporu�ujeme d�lat nativn� s podporou Rest-Api, ale umo�nit ti tvo�it jednoduch� ��d�c� aplikace pro pr�mysl a pr�myslov� ��zen� s prezentac� dat.

  * **Grid Apps**::
  * **Grid Widgets**::

  Grid se skl�d� s kolekce aplikac� - a s Widget�

* BLOCKO: TODO

* CLOUD:  TODO

---

### Registrace Hardwaru





---

### Prvn� program pro Hardware



---

### Nahr�t� programu na Hardware



---

### Prvn� Blocko Program





Prvn� Vlastn� Blo�ek

Integrace Blocko s Hardwarem

Prvn� vlastn� Instance

Prvn� Aplikace v Gridu

Prvn� vlastn� Widget

Integrace s Blocko

#### 

#### Konfigurace hardware

N�sleduj�c� dokumentace pom�h� u�ivateli p�i prvn�m spu�t�n� a z�kladn� konfiguraci nov� zakoupen�ch za��zen�. Bli��� informace a specifikace jednotliv�ch za��zen� lze nal�zt v [Hardwarov� dokumentaci](Odkaz na Hardwarovou docu). B�hem konigurace lze indentifikovat chov�n� za��zen� pomoc� LED signalizace, kterou za��zen� prov�d�. V�znam t�chto LED sign�l�, lze vyhledat v Hardvarov� dokumentaci jednotliv�ch typ� za��zen� v sekci [LED signalizace](/byzance_documentation/hardware_intro/hardware/iodag3e/led-signalizace.md)

