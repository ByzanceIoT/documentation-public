# Komunikace s portálem 

Zařízení IODA je připojeno k Internetu přímo pomocí Ethernetu, či přes jiného IODU bezdrátovou technologíí LOWPAN. Takto komunikuje s Portálem. K tomuto je vnitřně využívaná technologie MQTT. Každé koncové zařízení je v topologii MQTT označováno jako Client a Portál obsahuje rozhraní označováno jako Broker.

![](/assets/IMG_20180318_183038.jpg)

Zařízení se mohou pomocí LOWPAN síťovat do virtuálních sítí a tvořit mesh. Každá mesh síť potřebuje alespoň jeden border router, což je jiné zařízení, které přemosťuje LOWPAN síť do ethernetu.

#Jak nastavit připojení k portálu

Zařízení se s Portálem spojuje automaticky na základě výchozích údajů uložených v Bootloaderu. Je-li třeba změnit připojení k jinému Portálu, je možné k tomu využít například Command režim Bootloaderu.

**popis, jak získat username a password z Becki**


