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
{{ :lowpan:vp-6lowpan-udp.png |}}

Z grafu je patrné, že maximální přenosová rychlost je přibližně 10 kB/s. Dále je zde patrný vliv fragmentace dlouhých paketů (překročením určité délky dojde ke vzniku dalšího fragmentu => nutný přenos další hlavičky => snížení přenosové rychlosti).

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