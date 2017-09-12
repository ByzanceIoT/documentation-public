# Vstupy a výstupy

# AnalogIn

Read an external voltage applied to an analog input pin.

```cpp
AnalogIn ain(pin_name);
printf(”ain value = %3.3f%%\n”, ain.read());
```

## AnalogOut

Set the voltage of an analog output pin in the range of VSS to VCC.

```cpp
AnalogOut aout(pin_name);
aout.write(some_float);
```

## DigitalIn

Read the value of an digital input pin

```cpp
DigitalIn din(pin_name);
printf("pin has value : %d \n", din.read());
```

## DigitalOut

Configure and control a digital output pin

```cpp
DigitalOut dout(pin_name);
dout=1;
```

## DigitalInOut

Bidirectional digital pin, combination of DigitalIn and DigitalOut

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

Number of DigitalIn pins that can be read as one value.

```cpp
BusIn
```

## BusOut

Number of DigitalOut pins that can be written as one value.

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



