# Komunikační rozhraní

API popsané v této kapitole, slouží k propojení desky s počítačem a externími zařízeními.

##Serial

Tato funkce slouží k definici sériového rozhraní a komunikaci po sériové lince. Ke komunikaci jsou zapotřebí dva piny - RX(recieve data) a TX(transfer data)
```cpp
//Defince sériového rozhraní 
Serial pc(PIN_TX, PIN_RX);

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
Example
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



