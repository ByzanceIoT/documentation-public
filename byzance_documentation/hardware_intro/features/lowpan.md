#### Základní teoretické informace o použité technologii LoWPAN 

Článek se zabývá obecně technologií 6lowpan. 6lowpan je zkratka Low power Personal Area Network; číslice 6 značí, že přenos probíhá pomocí IPv6 paketů. 

Technologie je spjata s rozšířeným rádiovým rozhraním 802.15.4, což umožňuje využití hardwaru, který je na trhu již nějakou dobu a přechod na 6lowpan znamená pouze softwarovou úpravu. 

#### 6lowpan stack 
{{ :lowpan:lowpan_stack.jpg?200|6lowpan stack}}
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
K tomu je využito protokolu RPL (podrobněji viz. [[https://tools.ietf.org/html/rfc6550|RFC6550]]).

K teoretickému úvodu je super toto: {{:lowpan:6lowpan_demystifie_ti.pdf|6LoWPAN demystifie - Texas Instruments}}

A část informací je i zde a chtělo by to přepsat sem:
[[https://docs.google.com/document/d/1A-cqm9hOdHit5S7163-tDQGedfTgmsbwE1ObiNAx7fY/edit#|google docs]]