# Flash paměť obecně

Interní i externí paměť Byzance desek jsou typu \[\[https://cs.wikipedia.org/wiki/Flash\_pam%C4%9B%C5%A5\|FLASH\]\]. Neinicializovaná hodnota 32 bitových paměťových buněk je 0xFFFFFFFF \(samé logické 1\), přičemž zápisem lze logická 1 pouze vypnout na logickou 0. Pokud je třeba zapsat znovu do některé paměťové buňky logickou 1, je třeba dodržet přibližně následující postup

* Načtení aktuální stránky z FLASH do RAM
* Změna konkrétní informace v RAM
* Smazání stránky ve FLASH
* Zápis nové stránky z RAM do FLASH

Tento postup nese několik nevýhod

* Drobné změny trvají velmi dluho \(velký overhead\), protože kvůli každému byte je třeba pracovat s celou stránkou několika kB.
* Pokud dojde chybě mikrokontroléru mezi kroky "smazání FLASH" a "zápisem nové stránky", datová informace je nenávratně ztracena. Mezi takové chyby může patřit například zásek software, nebo výpadek napětí. Ztrátě dat je možné předejít \[\[memory:journal\|využitím žurnálu\]\].

Existují ale i výhody použití FLASH paměti

* Cena, kdy FLASH paměť je levnější než EEPROM

## Životnost

Při práci s externí pamětí je třeba dbát na životnost paměti, která není neomezená. Obecně se udává v řádu zhruba 100 tisíc přepisů, což může být problém například při kontinuálním logování, nebo chybnému zacykleném kódu, který bude stále přepisovat stejnou paměťovou buňku.

