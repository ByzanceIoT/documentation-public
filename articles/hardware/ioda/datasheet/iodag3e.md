# IODAG3E

IODAG3E je zařízení které umožňuje vzdálené programování a zároveň funguje jako IoT brána komunikující s Cloudem skrze ethernetové rozhraní. Vlastností tohoto zařízení je velké množství výstupních a vstupních periférií, které umožňují vysokou variabilitu využití jak v průmyslu, tak domácí automatizaci či v menších aplikacích.


![ioda_board](/images/hardware/IODAG3E.png)


## Mikroprocesor 

* STM32F437IIH6 \([Datasheet](http://www.st.com/content/ccc/resource/technical/document/datasheet/fd/8c/0a/19/13/8f/41/99/DM00077036.pdf/files/DM00077036.pdf/jcr:content/translations/en.DM00077036.pdf)\)
* 2 MB Flash
* 180 MHz
* 192 kB SRAM \(včetně 64 KB CCM\)
* Programování pomocí SWD nebo z Cloudu
* MAC adresa

## Periférie 

* Ethernet
* Lowpan
* GPIO Header (41 pinů) 
* A/D, D/A převodníky
* SPI 
* CAN
* UART
* I2C
* SAI
* USB 2.0

## Další funkce

* Online programování v C/C++ z webové aplikace Byzance
* Vzdálená aktualizace uživatelského programu
* Vestavěný webový server
* Konektor na uchycení Lowpan modulu WEXP pro bezdrátovou komunikaci
* Low power management
* Hardwarová akcelerace CRC, šifrování
* Hardwarový watchdog
* Automatické zálohování uživatelského programu a jeho obnova při selhání
* Možnost vestavění na vlastní PCB


## Možnosti napájení 

Zařízení disponuje efektivním spínaným zdrojem s širokým rozsahem vstupního napětí.

Lze napájet přes:

* MicroUSB 
* Externí zdroj 6-60V AC/DC
* POE (aktivní/pasivní)
* Napájení z baterie

## Tlačítka 

* Tlačítko pro RESET
* Tlačítko USER

## Led signalizace 

* RGB LED modul

## Rozměry a hmotnost
  
 * Rozměry desky včetně konektorů : 42,5 x 65,5 mm
 * Výška včetně konektorů: 11.5 mm
 * Hmotnost: 60g


