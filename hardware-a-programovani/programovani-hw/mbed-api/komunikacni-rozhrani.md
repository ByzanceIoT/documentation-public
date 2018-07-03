# Komunikační rozhraní

## Komunikační rozhraní

V této sekci jsou zdokumentované funkce MBED API sloužící ke komunikaci s počítačem a externími zařízeními.

## [Serial](https://os.mbed.com/docs/latest/reference/serial.html)

Tato třída slouží k využití sériového rozhraní a komunikaci po sériové lince. Ke komunikaci jsou zapotřebí dva piny - RX\(recieve data\) a TX\(transfer data\).

```cpp
#include "byzance.h"

Serial pc(X09, X11);

void init(){
    pc.baud(9600); //Nastavení baudové rychlosti
    pc.printf("Serial connection\n"); //Send to serial line
}

void loop(){
    pc.printf("Hello world\n");
}
```

## [SPI](https://os.mbed.com/docs/latest/reference/spi.html)

Komunikace pomoc SPI \(Serial Peripheral Interface\), rozlišuje komunikační prvky na Mastra a jeho podřízené jednotky - Slave. Každý Master může obsluhovat několik Slavů tím způsobem, že vyzve jednotku ke komunikaci přepnutím příslušného pinu SS \(Slave select\) do logické nuly a vyslání dotazu \(Bytu\). Jednotka Slave poté na tento dotaz odpovídá zpátky. Po ukončení komunikace Master přepne pin SS zpět do logické jedničky. Jednotka Slave nikdy neodesílá žádná data bez výzvy a Master vždy může komunikovat pouze s jedním Slavem najednou. Pro každý Slave má Master jeden příslušný digitální pin SS. Komunikační protokol je blíže vysvětlený například na [Wiki](https://en.wikipedia.org/wiki/Serial_Peripheral_Interface_Bus). 

### [SPI Master](https://os.mbed.com/docs/latest/reference/spi.html)

Příklad demonstruje využití sběrnice SPI pro čtení WHOAMI registru ze zařízení připojeného na sběrnici SPI na X konektoru. 

```cpp
#include "byzance.h"

Serial pc(SERIAL_TX, SERIAL_RX);    //For USB use: USBSerial pc(0x1f00, 0x2012, 0x0001, false); //
SPI spi(X14, X12, X10);  // mosi, miso, sclk
DigitalOut ss0(X08);    // Slave 0 select pin (Sometimes called CS - Chip Select)
​
void init(){
    spi.format(8,3);           // 8 bits, high steady state clock, second edge capture
    spi.frequency(1000000);    // Set clk frequency to 1 MHz
}
​
void loop(){     
    ss0 = 0;                          // Select the device by seting chip select low
    int whoami = spi.write(0x00);     // Send dummy byte to Slave and save received data
    ss0 = 1;                          // Deselect device
    pc.printf("WHOAMI register = 0x%X\n", whoami);    //Print the result
    Thread::wait(1000);
}
```

### [SPISlave](https://os.mbed.com/docs/latest/reference/spislave.html)

Příklad programu, který reaguje na přijatá data od SPI Mastera přičtením jedničky k přijatému Bytu

```cpp
#include "byzance.h"

Serial pc(SERIAL_TX, SERIAL_RX);
SPISlave device(X14, X12, X10, X08);   // mosi, miso, scl, ss (or CS - Chip select)


void init(){
	pc.baud(115200);
}

void loop(){
	// React if master send you a message
	if(device.receive()) {
		uint8_t v = device.read();    				// Read byte from master
	    pc.printf("Byte 0x%X recieved\n",v);		// Print it
	    device.reply(v+1);          			 	// Add one to received message and reply with it
	 }
}

```

## [I2C](https://os.mbed.com/docs/latest/reference/i2c.html)

Třída I2C poskytuje funkcionalitu I2C sběrnice v roli master. 

Příklad demonstruje jednoduché čtení teploty z teplotního čidla LM75BD.

```cpp
#include "byzance.h"

Serial pc(SERIAL_TX, SERIAL_RX);	//USBSerial pc(0x1f00, 0x2012, 0x0001, false); //
I2C i2c(X07, X06);	//sda, scl

const int addr8bit = 0x48 << 1; // 8bit I2C address, 0x90

void init(){
    i2c.frequency(400000);    //set clk frequency to 1 MHz
}

void loop(){
	// Read temperature from LM75BD
	char cmd[2];
	cmd[0] = 0x01;
	cmd[1] = 0x00;
	i2c.write(addr8bit, cmd, 2);

	Thread::wait(500);

	cmd[0] = 0x00;
	i2c.write(addr8bit, cmd, 1);
	i2c.read( addr8bit, cmd, 2);

	float tmp = (float((cmd[0]<<8)|cmd[1]) / 256.0);
	pc.printf("temperature = %.2f\n", tmp);
}
```

## [I2CSlave](https://os.mbed.com/docs/latest/reference/i2cslave.html)

Use to communicate with I2C Master.

```cpp
I2CSlave i2cslave;
```

## [CAN](https://os.mbed.com/docs/latest/reference/can.html)

Controller-Area Network bus standard support.

```cpp
CAN can;
```

