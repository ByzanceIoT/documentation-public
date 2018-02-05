# Komunikace po sériové lince \(UART\)

Zařízení Ioda umožňuje na své GPIO sběrnici definovat až 3 sériové linky, po kterých může komunikovat jak přímo s počítačem \(Např. se sériovým terminálem putty, termite\), tak s libovolnými zařízeními schopných stejné komunikace. Tato komunikaci slouží pouze k sériovému peer to peer přenosu dat a nelze na její linku připojit více jak dvě zařízení.

Obsah:

* [Zapojení](#zapojeni)
* [Inicializace](#inicializace)
* [Odesílání dat](#sent)
* [Zpracování dat](#zpracování-příchozích-dat)

## Zapojení {#zapojeni}

K zapojení sériové linky jsou potřeba pouze 3 vodiče připojené na piny RX, TX a GND, přičemž linky RX \(recieve data\) a TX \(Transfer data\) se kříží viz schéma

![](/images/hardware/uart_bus.jpg)

Při zapojování je nutné dbát na napěťové úrovně, které obě zařízení používají. Zařízení Ioda definuje logickou jedničku napěťovou úrovní 3,3V. V případě, že by aplikaci vyžadovala komunikaci například s Arduinem, které definuje logickou jedničku 5V, bylo by nutné mezi zařízení vsadit napěťový převodník, který sníží 5V Arduina na požadovaných 3,3V. V jiném případě by mohlo dojít k poškození Iody.

Na kterých pinech lze definovat sériovou linku lze zjistit z [dokumentace](//articles/hardware/ioda/datasheet/iodag3e/rozhrani-a-periferie.md) periférií zařízení IODAG3E.

## Inicializace

Po správném zapojení sériové linky je nutné v kódu linku inicializovat. Parametry inicializace sériové linky jsou 

* **Piny GPIO sběrnice na kterých se linka definuje** 
* **Rychlost přenosu (Baudrate)**
* **Formát**

První inicializace se provádí příkazem

```
#define pin_TX    Y00   // Y00 for UART4, could be for example X11 or SERIAL_TX 
#define pin_RX    Y01   // Y01 for UART4, could be for example X09 or SERIAL_RX

int baudrate = 115200;  // Depends on device - higher means faster (typically 9600, 28800, 57600 etc ..)

// Init serail line
Serial pc(pin_TX,pin_RX, baudrate);

```

Předchozí kód inicializuje sériovou linku pod názvem **pc** na pinech **Y00** a **Y01** s přenosovou rychlostí **115200** baudů za sekundu. Místo definovaných pinů je také možné použít makra **SERIAL_TX** a **SERIAL_RX**, které odkazují na piny totožné sériové linky, nebo libovolně vybrat jinou sériovou linku podle [dokumentace](//articles/hardware/ioda/datasheet/iodag3e/rozhrani-a-periferie.md).

Baudrate sériové linky můžeme dodatečně upravovat pomocí 

```
pc.baud(9600);
```

Sériová komunikace je tvořena takzvanými pakety, které se zkládají z několika bitů. Každý paket obsahuje start bit, datové bity, paritní bity a stop bity.  

![](/assets/UART-Packet.png)

**Formát** paketu musí být u obou komunikujících zařízení společně s **baudrate** definována **totožně**, jinak si zařízení neporozumí. 

Při inicializaci se defaultně nastaví 8 datových bitů, žádná parita a jeden stop bit. Pokud by aplikace či komunikace vyžadovala jiný formát, lze ho nastavit pomocí 


```
#define parity Odd     // Options: Even, None, Forced0, Forced1 

int data_bits = 8;   // has to be in range 5 - 8 
int stop_bits = 2;   // 1 or 2

pc.format(data_bits, Parity parity=SerialBase::None, stop_bits);
```





## Odeslání dat {#sent}

## Zpracování příchozích dat



