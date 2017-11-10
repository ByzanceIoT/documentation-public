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