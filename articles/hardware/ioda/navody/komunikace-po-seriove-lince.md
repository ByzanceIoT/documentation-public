# Komunikace po sériové lince \(UART\)

Zařízení Ioda umožňuje na své GPIO sběrnici definovat až 3 sériové linky, po kterých může komunikovat jak přímo s počítačem \(Např. se sériovým terminálem putty, termite\), tak s libovolnými zařízeními schopných stejné komunikace. Tato komunikaci slouží pouze k sériovému peer to peer přenosu dat a nelze na její linku připojit více jak dvě zařízení.

Obsah:

* [Zapojení](#zapojeni)
* [Inicializace](#inicializace)
* [Odesílání dat](#sent)
* [Zpracování dat](#zpracování-příchozích-dat)

## Zapojení {#zapojeni}

K zapojení sériové linky jsou potřeba pouze 3 vodiče připojené na piny RX, TX a GND, přičemž linky RX \(Recieve data\) a TX \(Transfer data\) se kříží viz schéma

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

Sériová komunikace je tvořena takzvanými pakety, které se skládají z několika bitů. Každý paket obsahuje start bit, datové bity, paritní bity a stop bity.  

![](/assets/UART-Packet.png)

**Formát** paketu musí být u obou komunikujících zařízení společně s **baudrate** definována **totožně**, jinak si zařízení neporozumí. 

Při inicializaci se defaultně nastaví 8 datových bitů, žádná parita a jeden stop bit. Pokud by aplikace či komunikace vyžadovala jiný formát, lze ho nastavit pomocí 


```
#define PARITY Odd     // Options: Even, None, Forced0, Forced1 

int data_bits = 8;   // Has to be in range 5 - 8 
int stop_bits = 2;   // 1 or 2

pc.format(data_bits, PARITY, stop_bits);
```

## Odeslání dat {#sent}

Odesílání dat po sériové lince 

## Zpracování příchozích dat

Ke zpracování příchozího znaku po sériové lince lze využít základní jednoduchý program.  

```

#include "byzance.h"
 
Serial pc(SERIAL_TX, SERIAL_RX); // tx, rx
Serial device(X11, X09);  // tx, rx
 
int main() {
    while(1) {
        if(pc.readable()) {
            device.putc(pc.getc());
        }
        if(device.readable()) {
            pc.putc(device.getc());
        }
    }
}

```

Pokud má hlavní program konat náročnější funkci, je nutné příchozí data zpracovávat asynchronně. V tomto případě lze využít toho, že příchozí znak vyvolá na procesu přerušení. Na toto přerušení lze připojit funkci, která příchozí znak zpracuje do bufferu a v případě, že je věta kompletní, nechat hlavní program tento buffer zpracovat. Příklad takového kódu může vypadat následovně


```
#include "byzance.h"

#define SERIAL_BUFFER_SIZE  100
#define BYZANCE_OVER_USB 	0

Serial serial(SERIAL_TX,SERIAL_RX); // tx, rx

MESSAGE_OUTPUT(message_out_counter, STRING);


// Global variables
char buffer[SERIAL_BUFFER_SIZE];
char line_buffer[SERIAL_BUFFER_SIZE+1];
char *parser;
int buff_pointer;
char c;
bool complete_line;
float voltage;
float temp;



/*
void read_line(){


	char line[SERIAL_BUFFER_SIZE];
	// disable interrupts for critical section
	NVIC_DisableIRQ(UART_IRQn);


	// process buffer


	ip = strtok(buffer,":");
	uptime = strtok(0,":");
	parser = strtok(0,":");
	voltage = atof(parser);
	parser = strtok(0,":");
	temp = atof(parser);

	buff_pointer = 0;

	serial.printf(" Voltage : %f , CPU TEMP %f", voltage+1, temp+2);

	// enable interrupts - end of the critical section
	NVIC_EnableIRQ(UART_IRQn);


}
*/

void rx_interrupt(){

	while((serial.readable()) && ((buff_pointer < SERIAL_BUFFER_SIZE) && (complete_line == 0))){

		// Read char from serial
		c = serial.getc();

		// detect end of line
		if ((c == ';') && (complete_line == 0)){

			complete_line = 1;

		}else if (complete_line == 0) {

			buffer[buff_pointer] = c;
			buff_pointer++;

		}
	}
}


void pre_init(){

	#if BYZANCE_OVER_USB
		ByzanceLogger::init(&usb);
	#else
		ByzanceLogger::init(&serial);
		serial.baud(115200);
	#endif

	ByzanceLogger::set_level(DEBUG_LEVEL_TRACE);
	ByzanceLogger::enable_prefix(false);

}

void init(){

	complete_line = false;

	serial.attach(&rx_interrupt, Serial::RxIrq);

}


void loop() {

	// If the line is ready copy buffer and process the line
	if (complete_line || (buff_pointer == (SERIAL_BUFFER_SIZE-1))){

		// Disable serial line interrupts
		NVIC_DisableIRQ(UART4_IRQn);

		if (buff_pointer > 0){
			memcpy(&line_buffer, &buffer,buff_pointer);
		}
		// Set buffer pointer
		complete_line = 0;
		buff_pointer = 0;

		// Enadble serial interrupts
		NVIC_EnableIRQ(UART4_IRQn);

		// process line

		//ip = strtok(line_buffer,":");
		//uptime = strtok(0,":");
		parser = strtok(line_buffer,":");
		voltage = atof(parser);
		parser = strtok(0,":");
		temp = atof(parser);

		serial.printf("%f % \n", voltage);
	}

    //serial->printf("ip=%s\n", Byzance::get_ip_address());
    Console::log("Test console\n");
    serial.printf("test console \n");

	Thread::wait(200);

}

```










