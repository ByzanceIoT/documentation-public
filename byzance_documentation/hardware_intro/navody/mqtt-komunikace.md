## MQTT komunikace 

**MQTT je** jednoduchý centralizovaný **protokol**, kde mezi sebou komunikují tři typy zařízení:
  * **broker** - centrální prvek sítě (server, PC)
  * **klient** - koncové zařízení (Yoda, device)
  * **gateway** - překladač mezi různými protokoly (volitelně).

Základem je systém typu **publish**  / **subscribe** (zveřejnit/odebírat). Klienti s funkcí **publish** odesílají zprávy do brokeru, který na základě přihlášených odběrů provede jejich třídění a přeposlání správným klientům. Zprávy také může odesílat i samotný broker. Předávání zpráv je pouze jednosměrné a jsou zvěřejňovány do tzv. **topiců** (témat).

V našem pojetí reprezentuje Homer server uzel typu //broker//, Yoda je kombinací uzlů //klient// a //gateway// a device je uzlem //klient//. Yoda překládá MQTT protokol a topicy pro device posílá přes náš proprietární protokol na device, kde je (zkrácená) MQTT zpráva zpracována. FIXME poslední věta možná už nebude platit.

#### Topics (témata) 
Zprávy jsou zveřejňovány do topiců, které mají hierarchickou strukturu. Struktura je plně definovatelná vývojářem a její podoba je níže. Jednotlivé úrovně hierarchie jsou oddělovány znakem „/“. Obecně MQTT zpráva vypadá takto:

příklad topicu ''nulta_uroven/prvni_uroven/druha/treti''

Samotná data spojená s daným topicem jsou přenášena pomocí JSONů a pokud je součástí část binárky, kóduje se pomocí BASE64.



#### Konvence pro názvy Byzance topiců 
##### In/out postfix 
V Byzance existují vždy **dva topicy se stejným názvem**, které se **liší postfixem**, např.: ''message_out'' a ''message_in''. Proč dva? V situaci, kdy klient pošle zprávu do topicu ''message'' a zároveň je přihlášen k odběru tohoto topicu, byla by mu obratem doručena zpráva, kterou sám vyslal. To je nežádoucí chování zvyšující zátež sítě.

Z tohoto důvodu klient publikuje zprávy do topicu s postfixem **_out** a je odebírá topicy koncovkou **_in**. 
Např. potřebuji v Yodovi aktualizovat čas a tak broker vygeneruej zprávu ve stylu ''yoda_XXXXXXXXXXXXXXXXXXXXXXXX/settings_in/datetime''. Yoda tento topic odebírá, zprávu přijme a pošle potvzení do stejného topicu, ale s koncovkou **_out**, tj ''yoda_XXXXXXXXXXXXXXXXXXXXXXXX/settings_out/datetime''.

Může se hodit vědět, že existují **zástupné symboly** „+“ nebo „#“. Znak „+“ slouží jako zástupný pro celou **jednu úroveň**, např. ''yoda_adresa/device/+/teplota'' slouží pro odebírání dat ze všech teplotních senzorů. Znak „#“ lze využít jako zástupný znak pro **všechny následující nižší úrovně**, tedy ''yoda_adresa/device/#''.
==== Adresace ====
Každé zařízení v projektu Byzance lze indentifikovat pomocí **jedinečné adresy** a ta je součástí názvu topiců:
  * **Yoda** - identifikuje se pomocí unikátního **24 bit [[hardware:full_id#Full ID|Full ID]]**, zapisuje se hexadecimálním stringem (např. 002600513533510B34353732).\\ Např. topic: ''yoda_002600513533510B34353732/settings_in/datetime''

  * **Device** - identifikátorem je opět [[hardware:full_id#Full ID|Full ID]] device. Do device se příkazy posílají přes nadřazeného Homera. Pokud má Device adresu 003E00523533510B34353732, příkaz se pošle např. do topicu ''yoda_002600513533510B34353732/device_in/003E00523533510B34353732/datetime''. FIXME adresování podle device nemusí do budoucna platit.

#### Hierarchická struktura topiců 
Seznam všech topiců používaných Byzance je na stránce [[topics:| MQTT Topics]].


===== Seznam topiců =====

Aktuální topicy, do kterých se subscribuje zařízení je uložen v souboru ByzanceClientRoutines.h
<code>
CLIENT_TOPIC_DIGITAL 	"/d_in/#"
CLIENT_TOPIC_ANALOG 	"/a_in/#"
CLIENT_TOPIC_MESSAGE	"/m_in/#"
CLIENT_TOPIC_COMMAND	"/command_in/#"
CLIENT_TOPIC_SETTINGS	"/settings_in/+"
CLIENT_TOPIC_INFO	"/info_in/+"
CLIENT_TOPIC_CONSOLE	"/console_in/#"
</code>

Prefix se definuje ve stejném souboru pod makrem
<code>
CLIENT_PREFIX           "" (už není)
</code>

==== Další informace ====

Další informace a podrobnosti je možné dohledat v příslušných sekcích topiců

  * [[Yoda:topic_byzance| MQTT Byzance topicy pro digital/analog/message zprávy]]  
  * [[Yoda:topic_commands| MQTT Topic Commands]]  
  * [[Yoda:topic_settings| MQTT Topic Settings]]  
  * [[Yoda:topic_info| MQTT Topic Info]]  
  * [[Yoda:topic_report| MQTT Topic Report]] 




