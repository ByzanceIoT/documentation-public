## Lowpan BR

Jedná se o hraniční router, který má za úkol zajistit směrování paketů (tj. na základě analýzy IP adresy a routovací tabulky přeposlat paket z jednoho rozhraní na druhé).


#### Architektura sítě 

{{ :feature:lowpanbr_arch.png?300 | Lowpan Border Router v síti}}
LowpanBR má dva síťové interfacy:
  * pro přístup k Internetu a LAN disponuje rozhraním WiFi nebo Ethernet
  * pro přístup k devicům (D) disponuje 6lowpan rozhraním

Prozatím se předpokládá pouze IPv4 konektivita k Internetu/LAN. Naproti tomu technologie 6lowpan ze své podstaty vytváří pouze IPv6 konektivitu. 

Pro přístup zařízení (D) k Internetu/LAN je používáno techniky NAT64, jež je implementována na LowpanBR. Jediným omezením této techniky je fakt, že spojení vždy musí navázat device (D), čímž je vytvořen záznam v NAT64 tabulce a směrování z/do Internetu již funguje obousměrně na základě analýzy portů. 

==== Příklad: navázání TCP spojení se vzdáleným serverem pomocí doménového jména ====
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

==== Jak zjistit hodnotu flagu Lowpan BR ====
  * V [[bootloader:overview|bootloaderu]] v [[bootloader:commands|command režimu]]
  * Zjištění pomocí příslušného [[yoda:topic_info|info topicu MQTT]] či nastavení v [[yoda:topic_settings|settings topicu]]
  * [[tutorial:public_functions|Veřejnou funkcí třídy Byzance]]
  * Ve [[tutorial:webview|webovém rozhraní]]

==== Softwarová architektura ====

Funkcionalita border routeru je rozdělena na čtyři části (zdrojové soubory):
  * třída LowpanBR
  * třída DNS64
  * ovladač stm32xx_emac
  * nat64_dri

=== LowpanBR ===
Jedná se o statickou třídu, která se inicializuje metodou ''init()''. Tato metoda vytvoří a spustí nové vlákno, kde nejprve dojde k inicializaci rádiového rozhraní, v případě úspěchu je spuštěn událostní systém v tomto vlákně. Postupně se tedy inicializuje lowpan interface v roli  border roteru a také backhaul interface (tunelovací ovladač). Pokud proběhne vše dle plánu, je inicializována DNS64 funkcionalita.

=== DNS64 ===
Metoda ''init()'' otevře soket nad rozhraním lowpan a zadaným portem (defaultně 53) a přiřadí callback, který je volán v případě události na soketu. V případě přijmu dat je vyhodnocen požadavek, pokud je validní (AAAA dotaz - na IPv6), je dotaz na doménové jméno replikován na backhaul interface (jako A dotaz - na IPv4). Pokud je IPv4 tázaného doménového jména úspěšně zjištěna, je generována AAAA odpověď a odeslána zpět tazateli.

=== stm32xx_emac ===
Jedná se o ethernetový ovladač a je součástí lwip. Ve své originální podobě neumožňuje implementaci NAT64 funkcionality. Byly zde provedeny následující změny:
  * přidaná funkce ''arm_tun_phy_device_register()'' - provede inicializaci tunelovacího ovladače  (nulování callbacků, které nastavuje vyšší vrstva, nastavení odesílacího callbacku)
  * přidaná funkce ''stm32_tun_phy_tx()'' - callback registrovaný při inicializaci ovladače; je automaticky volán vyšší vrstvou lowpan v případě, že je potřeba odeslat nějaká data
    * provede se kontrola integrity paketu, konverze, alokace bufferu a paket je odeslán pomocí původní funkce ''_eth_arch_netif_output_ipv4'' do ethernetu
  * funkce ''_eth_arch_rx_task'' běží ve vlastním (přijímacím) vlákně; původně prováděla výčet rámce do bufferu a jeho předání síťovému interfacu (netif) lwip; zde je provedena odbočka - nejdříve je vyhodnoceno, zda rámec patří do NAT64 nebo do lwip netif
    *  v případě, že rámec patří do lwip, je proveden původní kód
    *  v případě, že rámec patří do NAT64, je buffer překopírován do vlastního bufferu, konvertován a odeslán do lowpan routeru

=== nat64_dri ===
Jedná se o ovladač nat64 - provádí konverze paketů, udržuje tabulky (tcp a udp). 