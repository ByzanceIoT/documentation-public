# Rozšiřující moduly

Na [základní jednotky](../zakladni-jednotky/) se připojují v této kapitole rozebrané rozšiřující moduly \(shieldy\). Smyslem rozšiřujících jednotek je přinést konkrétní funkcionalitu bez nutnosti vyvíjet vlastní hardware. Jedná se o předpřipravené desky, které se pouze připojí na základní jednotky a bez dodatečné kabeléže nebo drátování na nepájivém poli lze vyzkoušet intereakci s reálným světem. Dobře slouží pro rychlé vytvoření ukázek na nejčastěji řešené aplikace jako je měření teploty a nebo spínání relé. Lze s nimi rychle bez větší námahy postavit funkční prototyp. Těmto jednotklám se alternativně říká **shieldy**.

[Základní jednotky](../zakladni-jednotky/) podporující připojení shieldů musí mít integrovaný tzv. X konektor \(např. [IODAG3E](../zakladni-jednotky/iodag3e/)\). Jde o standartní 20 pinový header s roztečí 2.54mm a rozložením 2x10 pinů \(samice\). Do tohoto headeru se připojují všechny shieldy. Rozložení a popis vstupů/výstupů X konektoru je [zde](../zakladni-jednotky/iodag3e/rozhrani-a-periferie.md#pinout).

### Rozměry

Shieldy existují ve dvou velikostech: plná a poloviční. Shield plné velikost má rozměry totožné jako základní jednotka [IODAG3E](../zakladni-jednotky/iodag3e/). Poloviční shield je zcela shodný s plným shieldem pouze s tím rozdílem, že má poloviční délku. Rozměrový nákres je níže \(v milimetrech\).

![](../../../.gitbook/assets/shields_both_sizes_dimensions.png)



### Kompatibilita shieldů

Každý z shieldů využivá určité datové piny z [X konektoru](../zakladni-jednotky/iodag3e/rozhrani-a-periferie.md#pinout) a zároveň žádný shield nevyužívá všechny najednou. Je tedy možné použít více shieldů najednou. V tétou sovislosti lze mluvit o kompatibilitě shiledů elektrické a mechanické.

#### Mechanická kompatibilita

Obecně lze shieldy na sebe skládat jako stavebnici a zapojovat jeden do druhého. Může se však stát, že např. [Ultrazvukový shield ](ultrasonic-shield.md)a [PIR shield ](pir-shield.md)na sebe dát nejdou. Nejdou na sebe dát z duvodu, že oba shieldy pro svou činnost potřebují volný prostor nad shieldem. Obdobně jiné shieldy mohou mít vysoké svorkovnice, které zabrání dalšímu skládání shieldů na sebe.

#### Elektrická kompatibilita 

Elektrická kompatibilita se odvíjí od sdílení pinů mezi jednotlivými shieldy. Jinými slovy jde o to, že jeden pin [X konektoru](../zakladni-jednotky/iodag3e/rozhrani-a-periferie.md#pinout) mohou využívat dva důzné shieldy a takové shieldy nebude možné použít najednou. Teoreticky to možné být může, ale přinese to komplikace ve firmware. Pro jednoduchost však mluvíme o tom, že **shieldy není možné použít najednou**, tzn. **shieldy nejsou spolu** komatibilní.

V případě elektrické kompatibility shieldů je dostupná tabulka kompatibility, kde je kompatibilita patrná. _**TODO: přidat pdf s tabulkou kompatibility**_

### Firmware

Zpravidla na všechny shieldy jsou vytvořený example projekty pro jednoduché vyzkoušení funcionality hardware. Všechny examply jsou dostupné v k tomu určeném repozitáři.



