# Flash paměť

Interní i externí paměť Byzance desek jsou typu [FLASH](https://cs.wikipedia.org/wiki/Flash_paměť), přičemž zápisem lze logická 1 pouze vypnout na logickou 0. Pokud je třeba zapsat znovu do některé paměťové buňky logickou 1, používá se mazání celých stránek a je třeba dodržet přibližně následující postup

* Načtení aktuální stránky z FLASH do RAM
* Změna konkrétní informace v RAM
* Smazání stránky ve FLASH
* Zápis nové stránky z RAM do FLASH

Tento postup nese několik nevýhod

* Drobné změny trvají velmi dluho \(velký overhead\), protože kvůli každému byte je třeba pracovat s celou stránkou několika kB.
* Pokud dojde chybě mikrokontroléru mezi kroky "smazání FLASH" a "zápisem nové stránky", datová informace je nenávratně ztracena. Mezi takové chyby může patřit například zásek software, nebo výpadek napětí. Ztrátě dat je možné předejít [využitím žurnálu](/byzance_documentation/hardware_intro/obecne/flash-pamet/zurnal.md).

Existují ale i výhody použití FLASH paměti

* Cena, kdy FLASH paměť je levnější než EEPROM

## Životnost

Při práci s externí pamětí je třeba dbát na životnost paměti, která není neomezená. Obecně se udává v řádu zhruba 100 tisíc přepisů, což může být problém například při kontinuálním logování, nebo chybnému zacykleném kódu, který bude stále přepisovat stejnou paměťovou buňku.

# Žurnál

Vzhledem k \[\[memory:flash\_tutorial\|obecné povaze fungování\]\] flash paměti může dojít ke ztrátě dat při jejich změně. Toto se může stát například v situaci, kdy je třeba změnit několik bytů dat, které jsou společně s celou stránkou načteny do RAM, změněny, stránka je ve FLASH paměti smazána a nahrazena novou změnou. Pokud mezi smazáním a nahrazením dojde k zaseknutí kódu, výpadku napájení nebo restartu, integrita dat je poškozena a zpravidla dochází ke ztrátě celé stránky. Této situaci lze předejít použitím žurnálu.

## Princip fungování žurnálu

Bezpečně je možné zapsat na jednu iteraci maximálně data o velikosti jednoho subsektoru \(4096 kB\). Toto omezení je softwarové. Z toho vyplývá velikost žurnálu, který je dvojnásobek jednoho subsektoru \(tedy 2\*4096 B\), protože data můžou mít sice velikost 4 KiB, ale můžou přesahovat z jednoho subsektoru do druhého. Dále se využívá žurnálový index, kde je uložena  informace o datech, které jsou právě v žurnálu. Jednotlivé rozsahy adresy a další podrobnosti jsou rozepsány v sekci \[\[memory:external\|externí paměti\]\].

Postup bezpečného zápisu do FLASH přes žurnál je následovný

* Data ze subsektorů, do kterých se bude zapisovat, jsou načtena do RAM. Tím pádem stále zůstávají uloženy ve FLASH paměti pro případ výpadku napájení.
* Část dat, která má být přepsána, se v RAM změní.
* Buffer se z RAM uloží do žurnálu. Pokud po tomto kroku dojde k výpadku napájení, aktuálně platná data jsou zdrojová a na žurnál se nebere ohled. V tom případě je zahozena nejnovější změna nad daty, ale původní data se neztratí.
* Do žurnál indexu se zapíše, že žurnál je platný. Pokud po tomto kroku dojde k výpadku napájení, při inicializaci driveru dojde k detekci nevyřízeného žurnálu a ten se začne bezpečně obnovovat, viz další kroky.
* Data se začnou z žurnálu kopírovat na místo určení. Po dokopírování jsou tedy stejná data redundantně v žurnálu i v místě určení. Pokud v této chvíli dojde k chybě při kopírování nebo výpadku napětí, žurnál index má poznamenáno, že platná data jsou v žurnálu a při obnovení napájení inicializace paměti detekuje, že žurnál nebyl vyřízen a začne data kopírovat znova. Nedojde tedy ke ztrátě.
* Jsou-li data z žurnálu zkopírována správně, žurnál index je smazán, čímž je dáno najevo, že celá operace je vyřízena. Data v žurnálu jsou tímto neplatná a data v místě určení jsou v tomto kroku již platná. Integrita je zachována a operace je dokončena.



