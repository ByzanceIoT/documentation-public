# 6LowPAN

## Architektura



![](../../.gitbook/assets/image%20%281%29.png)

\#TODO lepší obrázek sítě \(lowpanbr + lowpan uzly\)

### Zařízení Border Router

Jedná se o hraniční router, který má za úkol zajistit směrování paketů z/do bezdrátové sítě. Má tedy ze své podstaty dvě komunikační rozhraní:

* bezdrátové s technologií 6LowPAN
* obecný vstup do Internetu \(například [GSM](gsm.md), Ethernet\)

Zařízení tohoto typu samo o sobě vytváří bezdrátovou síť a je tedy jakýmsi středobodem sítě. Pro využití je nutné [nakonfigurovat](../sprava-zarizeni/konfigurace-zarizeni.md) zařízení tak, aby byla zapnutá funkcionalita _lowpanbr_ a byl [specifikován zdroj Internetu](specifikace-zdroje-internetu.md).

### Zařízení Router

Jedná se o uzel bezdrátové sítě, aktivně využívá právě jedno komunikační rozhraní. Připojuje se k již existující síti vytvořené Border Routerem. Zařízení umožňuje přeposílat datové zprávy ostatním uzlům v síti, čímž lze navyšovat oblast pokrytí. 

Pro využití této funkcionality je nutné [specifikovat zdroj Internetu](specifikace-zdroje-internetu.md) jako _6lowpan_.

## Zabezpečení

Přístup k síti je zabezpečen a komunikace v rámci sítě je šifrovaná předsdíleným klíčem. Tento klíč je nutné doručit všem prvkům sítě.

## Vytvoření sítě

Pro vytvoření sítě jsou potřeba alespoň dvě zařízení a to:

* zařízení typu Border Router \(IODA + WEXP\)
* zařízení typu Router \(IODA + WEXP, \#TODO bezdrátový prvek\)

Na zařízení typu Border Router je nutné nastavit flag lowpanbr=1 a vybrat nějaký netsource \(Ethernet, GSM\). Dále je potřeba nastavit jméno a heslo sítě, které zařízení vytváří.

Na zařízení typu Router je nutné nastavit příslušný netsource=6lowpan a dále pak údaje k síti, ke které se má zařízení připojit \(jméno a heslo totožné s nastavením na Border Router\).

