# Volatilní paměť

Voalitní paměť je na mikrokontrolérech STM32 tvořena jedním či dvěma moduly:

## RAM

plnohodnotná paměť pro náhodný přístup

## CCM \(Core Coupled Memory\)

Jedná se o neplnohodnotnou RAM, její omezení plyne především z toho, že není schopna pracovat s DMA; lze ji například použít pro různé překladové tabulky, jejichž výčet z paměti FLASH by byl časově náročný a je proto proveden jen jednou při startu procesoru

# Rozložení paměti v C a linkování

Z hlediska programování v jazyce C je možné rozdělit proměnné dle platnosti:

* globální - definice vně složeného příkazu
* lokální - definice uvnitř složeného příkazu
* statické - definice s klíčovým slovíčkem ''static''
* dynamické - alokováno funkcí \(např. malloc\)
* konstantní - definice s klíčovým slovíčkem ''const''

Z hlediska toho, zda jsou proměnné inicializované:

* inicializované
* neinicializované

C překladač využívá několik oblastí pro práci s pamětí:

* .bss - RAM; má pevnou velikost, oblast je nulována
* .data - RAM; má pevnou velikost, oblast je inicializována kopírováním z paměti FLASH
* stack + heap - zbylé volné místo v RAM, přičemž oblast pro heap je zaplňována od nejnižší adresy výše a stack od nejvyyší adresy níže
* .text - FLASH, oblast pouze pro čtení

Proměnné dle typu jsou přiřazeny do jednotlivých oblastí dle následující tabulky

|  | globální | lokální | statická | konstantní |
| :--- | :--- | :--- | :--- | :--- |
| inicializovaná | .data+flash | stack | .data + flash | flash |
| neinicalizovaná | .bss | stack | .bss | flash |

Do oblasti .bss tedy míří statické a globální neinicializované proměnné. Tyto proměnné musí být přístupné po celý běh programu a je znám jejich počet a datové typy a tedy i celková velikost. Vzhledem k faktu, že proměnné nejsou inicializované, není třeba nikde ukládat jejich inicializační hodnotu ve nevoalitní paměti \(FLASH\). Z hlediska využití paměti není prakticky rozdíl mezi globální a statickou proměnnou, přestože statická proměnná je platná pouze v použitém souboru.

Oblast .data je podobná oblasti .bss, s tím rozdílem, že jsou zde uloženy inicializované globální a statické proměnné. Bezprostředně po spuštění programu je tato oblast zaplněna svým inicializačním klonem z nevoalitní paměti \(FLASH\).

Oblast stack a heap vyplňuje zbytek paměti RAM. Stack je využíván pro lokální proměnné v jednotlivých složených příkazech - inicializací proměnných je stack postupně zvětšován, koncem složeného příkazu jsou jednotlivé funkce opět dealokovány ze stacku =&gt; dealokace probíhá ve opačném pořadí jako alokace, nezpůsobuje tedy fragmentaci paměti. Oblast heap je určena pro dynamickou alokaci \(například pomocí ''malloc\(\)''\), její alokace i dealokace je plně v režii programátora a nevhodnou skladbou alokací/dealokací může způsobit rozsáhlou fragmentaci paměti.

Oblast .text je určená pro read-only \(nebo alespoň read-mostly\) operace. Čtení z této paměti může být pomalejší.

