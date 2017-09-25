# Vstupy a výstupy

# AnalogIn

Převede napětí na pinu analogového vstupu v rozmezí 0 - 3.3V do digitální podoby a interpretujep ho číslem na škále 0-4095. Rozlišení převodníku je 2.44 mV. 

```cpp
AnalogIn ain(pin_name);
printf(”ain value = %3.3f%%\n”, ain.read());
```

## AnalogOut

Nastaví napětí na pinu analogového výstupu v rozmezí 0 - 3.3V zadáním hodnoty 0-4095. Každá jednotka interpretuje 2.44mV.

```cpp
AnalogOut aout(pin_name);
aout.write(some_float);
```

## DigitalIn

Přečte hodnotu digitálního vstupu

```cpp
DigitalIn din(pin_name);
printf("pin has value : %d \n", din.read());
```

## DigitalOut

Nastaví na digitálním vástupu logickou úroveň.

```cpp
DigitalOut dout(pin_name);
dout=1;
```

## DigitalInOut

Obousměrný digitální pin, kombinace digitálního vstupu a digitálního výstupu. 

```cpp
DigitalInOut diout(pin_name);

// configure as output
diout.output();

// set HIGH
diout = 1;

// configure as input
diout.input();

// read value of pin
pc.printf("diout value = %d \n", diout.read());
```

## BusIn

Umožňuje definovat seznam digitálních pinů, jejichž hodnota lze přečíst jako jedno číslo. 

 
```cpp

// Tři přepínače vedené jako BUS připojené na vstupy X1,X2,X3
BusIn switches(X01,X02,X03);

int init(){
//Nastavení módu přepínačů (PullUp/PullDown/PullNone/OpenDrain)
switches.mode(PullNone);


}

int main(){


while(1){


}



}
```

## BusOut

Definuje seznam digitálních výstupů, které lze přepsat jedním číslem. 

```cpp
BusOut
```

## BusInOut

Number of DigitalInOut pins that can be read and written as one value.

```cpp
BusInOut
```

## PortIn

Similar to BusIn, much faster but much less flexible.

```cpp
PortIn
```

## PortOut

Similar to BusOut, much faster but much less flexible.

```cpp
PortOut
```

## PortInOut

Similar to BusInOut, much faster but much less flexible.

```cpp
PortInOut
```

## PwmOut

Interface to control the frequency and mark-to-space ration of digital pulse train.

```cpp
PwmOut
```

## InterruptIn

Trigger an event when a digital input pin changes.

```cpp
InterruptIn
```



