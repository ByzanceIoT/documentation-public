# Komunikační rozhraní

## Komunikační rozhraní

V této sekci jsou zdokumentované funkce MBED API sloužící ke komunikaci s počítačem a externími zařízeními.

## Serial

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

## SPI

Serial Peripheral Interface Master.

See [https://en.wikipedia.org/wiki/Serial\_Peripheral\_Interface\_Bus](https://en.wikipedia.org/wiki/Serial_Peripheral_Interface_Bus)

```cpp
#include "byzance.h"
SPI spi(X14, X12, X10); // mosi, miso, sclkDigitalOut cs( X08);void init(){    spi.format(8,3);           //8 bits, high steady state clock, second edge capture    spi.frequency(1000000);    //set clk frequency to 1 MHz}void loop(){         cs = 0;          //select the device by seting chip select low    spi.write(0x8F); //send 0x8f, the command to read the WHOAMI register    int whoami = spi.write(0x00);   //send dummy byto to receive data    cs = 1;          //deselect device    printf("WHOAMI register = 0x%X\n", whoami);    //print the result    Thread::wait(1000);}      
```

## SPISlave

Serial Peripheral Interface Slave.

```cpp
SPISlave spislave;
```

## I2C

I2C Master functionality.

```cpp
I2C i2c;
```

## I2CSlave

Use to communicate with I2C Master.

```cpp
I2CSlave i2cslave;
```

## CAN

Controller-Area Network bus standard support.

```cpp
CAN can;
```

