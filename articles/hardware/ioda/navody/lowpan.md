#### Základní teoretické informace o použité technologii LoWPAN 

Článek se zabývá obecně technologií 6lowpan. 6lowpan je zkratka Low power Personal Area Network; číslice 6 značí, že přenos probíhá pomocí IPv6 paketů. 

Technologie je spjata s rozšířeným rádiovým rozhraním 802.15.4, což umožňuje využití hardwaru, který je na trhu již nějakou dobu a přechod na 6lowpan znamená pouze softwarovou úpravu.

#### 6lowpan stack
![6lowpan stack](/images/hardware/lowpan_stack.jpg)

6lowpan protokolový stack definuje především fyzickou, linkovou a síťovou vrstvu.

#### Fyzická vrstva
Je definována rozhraním 802.15.4. V této oblasti stojí především za zmínku, že provoz je možný v několika frekvenčních pásmech (868 MHz, 902 MHz, 2,4 GHz) a pomocí několika modulací.

#### Linková vrstva
Linková vrstva obecně řeší komunikaci mezi sousedy. V podvrstvě MAC déle řeší kontrolu přístupu k médiu. Data je možné šifrovat pomocí předsdíleného klíče (PSK) a to v sedmi úrovních. Přístup k médiu je řízen metodou CSMA/CA - naslouchání nosné s přecházením kolizí (vysílání do kanálu ve stavu idle, potvrzování zpráv).

#### 6lowpan přizpůsobovací vrstva 
Vzhledem k omezením daných nižší vrstvou 802.15.4 (maximální délka rámce, rychlost) a vyšší vrstvou (délka IPv6 hlavičky, jiné MTU) je nutné zavést přizpůsobovací vrstvu. Samotná 6lowpan vrstva má za úkol:
  * přizpůsobit MTU (IPv6 a 802.15.4) - fragmentace a následné skládání dlouhých paketů 
  * snížit délku paketu (komprese IPv6 hlavičky)
  * podporu routování v lowpan síti

#### Síťová vrstva 
Síťová vrstva je přímo IPv6. Oproti IPv4 byla hlavička paketu velmi zjednodušena - nese pouze informaci o verzi (6), délce payloadu, flow label, hop limit (ttl), kód další hlavičky a samozřejmě adresy (zdroj, cíl). Vzhledem k faktu, že adresy jsou 16bajtové, byla délka hlavičky, i přes zjednodušení oproti IPv4, prodloužena. 

#### Vyšší vrstvy 
Vyšší vrstvy je možné používat v podstatě stejně, jak je zvykem (stojí nad IPv6). Pro efektivní využití sítě je ovšem nutné dbát na redukci přenášených informací (používat binární protokoly místo textových, texty co možná nejvíce zkracovat atp.). 

#### Role a zařízení 
V rámci sítě existuje několik druhů zařízení:
  * border router - koordinátor sítě - provádí veškeré směrování (výpočet routovacích tabulek pro celou síť), nemůže přejít do režimu sleep; jedná se o vstupní bránu do IPv6 a potažmo IPv4 sítě
  * router - má svou vlastní routovací tabulku (od border routeru), podle může být prováděno směrování tj. přijme zprávu a doručí jí jinému routeru nebo hostu (pokud příjemcem není sám router)
  * host - zařízení nemůže směrovat (nemá routovací tabulku; snížení energetické náročnosti), ale samo o sobě může kdykoli vysílat a přijímat
  * sleepy host - toto zařízení také nemůže směrovat, oproti hostu navíc může vypnout svůj vysílač/přijímač a zprávy 

#### Routování 
Routováním se rozumí automatická tvorba routovacích tabulek pro každé zařízení, které routuje (border router, router). Každý bod v síti musí být odkudkoli dosažitelný (v každé tabulce musí být všechny body sítě).
K tomu je využito protokolu RPL ([podrobněji](https://tools.ietf.org/html/rfc6550|RFC6550)).

K teoretickému úvodu je super toto: [Texas Instruments](https://www.scribd.com/document/321983296/6LoWPAN-pdf)



A část informací je i zde a chtělo by to přepsat sem: [google docs](https://docs.google.com/document/d/1A-cqm9hOdHit5S7163-tDQGedfTgmsbwE1ObiNAx7fY/edit#)


## Lowpan BR

Jedná se o hraniční router, který má za úkol zajistit směrování paketů (tj. na základě analýzy IP adresy a routovací tabulky přeposlat paket z jednoho rozhraní na druhé).

#### Architektura sítě 

![Lowpan architecture](/images/hardware/lowpanbr_arch.png)

LowpanBR má dva síťové interfacy:
  * pro přístup k Internetu a LAN disponuje rozhraním WiFi nebo Ethernet
  * pro přístup k devicům (D) disponuje 6lowpan rozhraním

Prozatím se předpokládá pouze IPv4 konektivita k Internetu/LAN. Naproti tomu technologie 6lowpan ze své podstaty vytváří pouze IPv6 konektivitu. 

Pro přístup zařízení (D) k Internetu/LAN je používáno techniky NAT64, jež je implementována na LowpanBR. Jediným omezením této techniky je fakt, že spojení vždy musí navázat device (D), čímž je vytvořen záznam v NAT64 tabulce a směrování z/do Internetu již funguje obousměrně na základě analýzy portů. 

#### Příklad: navázání TCP spojení se vzdáleným serverem pomocí doménového jména

V tomto případě je nutné uvažovat tři záchytné body - D (device - iniciátor spojení), LowpanBR (hraniční router poskytující internetové připojení D), vzdálený server (například www.example.com, port 80).

  * D iniciuje spojení - prvně musí zjistit cílovou IP adresu z doménového jména
  * D se zeptá LowpanBR pomocí standartního AAAA dotazu na IPv6 adresu serveru www.example.com svého DNS serveru (LowpanBR)
  * LowpanBR vyhodnotí dotaz (komponenta DNS64) a zeptá se pomocí standartního A dotazu na IPv4 adresu svého DNS serveru (přiřazený z Ethernetu/WiFi pomocí DHCP serveru)
  * LowpanBR ze standartní A odpovědi získá IPv4 adresu serveru www.example.com
  * dále k této adrese přidá NAT64 prefix a vygeneruje standartní AAAA odpověď, kterou odešle zpět D
  * D nyní zná IPv6 adresu serveru www.example.com
  * D zahájí spojení s www.example.com - pošle první paket, jako cílovou adresu vyplní adresu získanou pomocí DNS dotazu, jako zdrojovou adresu použije svou IPv6 adresu, cílový port zvolí 80 a zdrojový port je obvykle náhodně generován
  * pomocí směrování je zajištěno, že tento paket (obsahující NAT64 prefix) je v LowPAN síti směrován do LowpanBR
  * LowpanBR detekuje v adrese NAT64 prefix, v příslušné NAT tabulkce (pro TCP spojení) vytvoří záznam - zapíše zdrojový port, zdrojovou IPv6 adresu, cílovou IPv4 adresu (tj. bez NAT prefixu)
  * aby bylo předejito kolizím, je zdrojový port změněn na unikátní a zapsán na stejný řádek NAT tabulky (pseudoport)
  * LowpanBR odešle IPv4 paket, jako zdrojovou adresu použije svou vlastní IPv4 adresu, zdrojový port je pseudoport, cílový port je nezměněn (80) a cílová adresa IPv4 je bez původní cílová adresa bez NAT64 prefixu
  * díky cílové adrese je paket směrován na server
  * server vygeneruje odpověď - tj. prohodí zdrojovou a cílovou adresu a zdrojový a cílový port
  * tato odpověď je pomocí IPv4 směrována na LowpanBR
  * LowpanBR najde v NAT tabulce záznam (dle zdrojové IPv4, cílového portu - pseudoportu a zdrojového portu - 80)
  * z tabulky zjistí IPv6 adresu cíle (D) a původní zdrojový port (přepsaný pseudoportem)
  * LowpanBR generuje IPv6 paket do LowPAN sítě - jako zdrojovou adrsu použije IPv4 adresu serveru s přidanmým NAT64 prefixem, cílová adresa je IPv6 adresa D dle tabulky, cílový port je původní zdrojový port (přeložen dle tabulky) a zdrojový port je 80
  * v LowPAN síti je dle cílové IPv6 adresy automaticky zajištěno směrování paketu k D


Napsat nějakou dokumentaci k tomu, co je Lowpan BR.

#### Jak zjistit hodnotu flagu Lowpan BR
  * V [[bootloader:overview|bootloaderu]] v [[bootloader:commands|command režimu]]
  * Zjištění pomocí příslušného [[yoda:topic_info|info topicu MQTT]] či nastavení v [[yoda:topic_settings|settings topicu]]
  * [[tutorial:public_functions|Veřejnou funkcí třídy Byzance]]
  * Ve [[tutorial:webview|webovém rozhraní]]

#### Softwarová architektura 

Funkcionalita border routeru je rozdělena na čtyři části (zdrojové soubory):
  * třída LowpanBR
  * třída DNS64
  * ovladač stm32xx_emac
  * nat64_dri

#### LowpanBR 
Jedná se o statickou třídu, která se inicializuje metodou ''init()''. Tato metoda vytvoří a spustí nové vlákno, kde nejprve dojde k inicializaci rádiového rozhraní, v případě úspěchu je spuštěn událostní systém v tomto vlákně. Postupně se tedy inicializuje lowpan interface v roli  border roteru a také backhaul interface (tunelovací ovladač). Pokud proběhne vše dle plánu, je inicializována DNS64 funkcionalita.

#### DNS64
Metoda ''init()'' otevře soket nad rozhraním lowpan a zadaným portem (defaultně 53) a přiřadí callback, který je volán v případě události na soketu. V případě přijmu dat je vyhodnocen požadavek, pokud je validní (AAAA dotaz - na IPv6), je dotaz na doménové jméno replikován na backhaul interface (jako A dotaz - na IPv4). Pokud je IPv4 tázaného doménového jména úspěšně zjištěna, je generována AAAA odpověď a odeslána zpět tazateli.

#### stm32xx_emac 
Jedná se o ethernetový ovladač a je součástí lwip. Ve své originální podobě neumožňuje implementaci NAT64 funkcionality. Byly zde provedeny následující změny:
  * přidaná funkce ''arm_tun_phy_device_register()'' - provede inicializaci tunelovacího ovladače  (nulování callbacků, které nastavuje vyšší vrstva, nastavení odesílacího callbacku)
  * přidaná funkce ''stm32_tun_phy_tx()'' - callback registrovaný při inicializaci ovladače; je automaticky volán vyšší vrstvou lowpan v případě, že je potřeba odeslat nějaká data
  * provede se kontrola integrity paketu, konverze, alokace bufferu a paket je odeslán pomocí původní funkce ''_eth_arch_netif_output_ipv4'' do ethernetu
  * funkce ''_eth_arch_rx_task'' běží ve vlastním (přijímacím) vlákně; původně prováděla výčet rámce do bufferu a jeho předání síťovému interfacu (netif) lwip; zde je provedena odbočka - nejdříve je vyhodnoceno, zda rámec patří do NAT64 nebo do lwip netif
  *  v případě, že rámec patří do lwip, je proveden původní kód
  *  v případě, že rámec patří do NAT64, je buffer překopírován do vlastního bufferu, konvertován a odeslán do lowpan routeru

#### nat64_dri 

Jedná se o ovladač nat64 - provádí konverze paketů, udržuje tabulky (tcp a udp). 


## 6Lowpan

Článek pojednává o využití bezdrátové sítě Lowpan pro přístup k Internetu nebo LAN síti. Jedná se tedy o alternativu k připojení přes Ethernet (nutná kabeláž) či WiFi (omezený rozsah). Tato síť je typu mesh a je tedy možné ji prostorově rozšiřovat (pro připojení k síti je nutné být v dosahu alespoň jednoho zařízení, které je již součástí sítě). 

#### Základní podmínky 

Pro vytvoření sítě je zapotřebí:
  * jednoho zařízení typu border router (viz. [[feature:lowpanbr|Lowpan BR]])
  * alespoň jednoho zařízení s rozšiřujícím modulem WEXP a nastaveným NETSOURCE na LOWPAN (device)

LowpanBR se chová jako základní stavební kámen sítě - vytváří ji a zároveň poskytuje konektivitu do LAN/Internetu. Device musí být samozřejmě v dosahu LowpanBR, každý další device v síti musí být v dosahu LowpanBR nebo jiného devicu.

#### Možnosti využití 

Zařízení chová prakticky stejně jako při připojení přes Ethernet či WiFi, LowPAN síť ovšem dosahuje nižších přenosových rychlostí. Jako MQTT hostname lze nastavit IPv4 adresu či přímo hostname MQTT brokeru. 

Dále je nutné brát v úvahu, že zařízení je připojené k IPv6 síti, není tedy divu, že výpis IP adresy vrací IPv6. Tento fakt je nutné brát v úvahu i v případě, že je vytvářen vlastní soket, který je zpravidla verze IPv6 - cílová adresa musí tedy být verze 6 i v případě komunikace s IPv4 zařízením, tuto adresu je nutné generovat na základě na NAT64 prefixu (12 B) a cílové IPv4 adresy (4 B) - celkem tedy 16 B (tj standartní délka IPv6 adresy).

Vzhledem k využití techniky NAT64 pro překlad z/do IPv4/IPv6 sítě, není možné, aby iniciátor spojení byl mimo LowPAN síť. To například znemožňuje využití http serveru na devicu. 

#### Nastavení v bootloaderu 

Výběr netsource:
  * příkazem ''netsource=3'' se nastaví jako netsource na LowPAN

Hodnoty pro MQTT hostname:
  * ''normal_mqtt_hostname=alpha.homer.stage.byzance.cz'' v pořádku, využito DNS služby LowpanBR
  * ''normal_mqtt_hostname=192.168.0.23'' je v pořádku, k IPv4 adrese bude přidán NAT64 prefix
  * ''normal_mqtt_hostname=abcd::100a'' není v pořádku, externí IPv6 komunikace není v současnosti dostupná

Dále je vhodné ujistit se, že není zapnuta funkcionalita LowpanBR:
  * ''lowpanbr'' v případě 1, je funkcionalita zapnutá
  * ''lowpanbr=0'' funkcionalitu vypne
Pozn.: Netsource má přednost před konfigurací LowpanBR. V případě, že je funkcionalita LowapnBR zapnutá a netsource je nastaven na LowPAN, není LowpanBR funkcionalita inicializována.

#### Nastavení zabezpečení 

todo

#### Softwarová architektura 
Je primárně využito mbed mesh-api, které poskytuje NetworkInterface (je tedy možné zacházet s tímto rozhraním stejně jako například s ethernetem). Byly provedeny drobné modifikace:
  * nd_tasklet - statická konfigurace
  * LoWPANNDInterface - původní část kódu pro připojení (metoda connect) není možné opakovat - nelze tedy zjistit, zda již došlo k připojení k síti; řešením je přesunutí této části kódu do inicializace, metoda connect v podstatě tedy jen vrací stav připojení a připojení je prováděno již při inicializaci

## Výsledky měření přenosové rychlosti a dosahu 


### Přenosová rychlost 

####Podmínky měření 

Test rychlosti byl prováděn za následujících podmínek:
  * měření probíhalo mezi dvěma prvky, oba byly součástí 6lowpan sítě (a byly to jediné prvky v síti)
  * měření probíhalo nad UDP sokety (tj. nebyla zde žádná nadbytečná data - potvrzování atp.)
  * ztrátovost paketů byla minimalizována (komunikace na velmi blízkou vzdálenost)
  * v každé iteraci byla zvětšována velikost paketu
  * v každé iteraci byl paket odeslán vícekrát a byl měřen čas odesílání celé skupiny
  * jako objem dat pro výpočet přenosové rychlosti byla použita délka UDP payloadu
  * měřeno na Nucleo 429ZI + Wireless Xplained Pro


#### Výsledky měření 

Maximální přenosová rychlost je přibližně 10 kB/s. Dále je zde patrný vliv fragmentace dlouhých paketů (překročením určité délky dojde ke vzniku dalšího fragmentu => nutný přenos další hlavičky => snížení přenosové rychlosti).

#### TCP komunikace 
  * TCP komunikace oproti UDP komunikaci přidává mj. spojovou komunikaci (tj. navazování spojení, ukončování spojení) a dále zvyšuje spolehlivost spojení potvrzováním odeslaných zpráv
  * komunikace je tedy oproti UDP zatížena zprávami pro navázání, udržování a ukončování spojení, ale především potvrzovacími zprávami
  * to vše má za následek citelné snížení přenosové rychlosti, obvzlášť v poloduplexních sítích (kterou 6lowpan je)

#### MQTT komunikace   
  * měřeno na YodaG3 + WEXP
  * MQTT komunikace standartně probíhá nad TCP
  * nad TCP je tedy navázáno spojení, které je udržováno pomocí keepalive zpráv (které zajišťují i otevírání NATu atp.), případně je spojení ukončeno
  * každá MQTT zpráva s sebou nese 3 TCP zprávy (vlastní MQTT zpráva, potvrzení a potvrzení přijetí potvrzení)
  * MQTT disponuje dále několika úrovněmi QoS, přičemž se tyto úrovně liší počtem potvrzovacích zpráv (tato potvrzení nemají nic společného s TCP potvrzováním - z hlediska TCP se jedná o normální zprávy jako každé jiné)
  * kombinace TCP a MQTT s vysokou úrovní QoS může mít za následek velmi dramatické snížení přenosové rychlosti (např. QoS2 1 zpráv = 1 zpráva + 2 potvrzovací a 1 TCP zpráva = 1 zpráva + 2 potvrzení, z čehož plyne, že na 1 MQTT zprávu je nutné přenést (1+2)*(1+2) = 9 paketů)
  * přenos binárního souboru o velikosti 450 kB pomocí MQTT zabere přibližně 3:30 minuty, tj. průměrná přenosová rychlost je tedy 2,1 kB/s (tj. přibližně pětina oproti UDP komunikaci) pro QoS1 na Windows
  * přenos binárního souboru o velikosti 450 kB pomocí MQTT zabere přibližně 3:08 minuty pro QoS1 na Linuxu (TCP komunikace na Linuxu respektuje zařízením vyžádané Maximum Segment Size = 300)
  * přenos binárního souboru o velikosti 450 kB pomocí MQTT zabere přibližně 3:10 minuty pro QoS0 na Windows
  * přenos binárního souboru o velikosti 450 kB pomocí MQTT zabere přibližně 2:20 minuty pro QoS0 na Linuxu, efektivní rychlost je tedy 3,21 kB/s

#### Dosah 
orientační dosah bez antén:
  * 0 nm
orientační dosah s anténami (pigtail 433 MHz, antény 868 MHz):
  *  přes jednu stěnu více jak 10 m
  *  přes dvě stěny cca 10 m (v případě shodné polarizace)

vývojová destička od Atmelu (myšleno stejné pokusy s destičkami Atmel na obou stranách):
  * výsledky jsou srovnatelné, destička od Atmelu má možná o něco lepší parametry

S pravděpodobně lepšími anténami dosahujeme srovnatelných nebo o něco horších výsledků. Může to být dáno ručním pájením (zbytky pasty, studené spoje), nevhodnými součástkami (pigtail, kondenzátor, anténní konektor), případně návrhem.
