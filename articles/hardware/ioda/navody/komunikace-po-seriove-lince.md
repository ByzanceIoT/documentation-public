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

Po správném zapojení sériové linky je nutné v kódu

## Odeslání dat {#sent}

## Zpracování příchozích dat



