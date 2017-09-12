# MBED API

MBED je open-source operační systém a sada knihoven vyvíjených konsorciem ARM. Je možné jej stáhnout [z Githubu](https://github.com/ARMmbed/mbed-os). Byzance k MBED přidává vlastní targety, definici pinů a nad MBED běží další služby v mikrokontroléru, které se starají o aktualizaci firmware a komunikaci se servery. Součástí MBED jsou knihovny pro BLE, LWIP, mbedTLS, nanostack a další.

Dokumentace k nejnovějšímu API je dostupná [na webu projektu](https://docs.mbed.com/docs/mbed-os-api-reference/en/latest/).

# Vstupně/výstupní API

## AnalogIn

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

# Digital interface APIs

## Serial

Generic serial protocol API, send and receive data.

See \[\[[https://en.wikipedia.org/wiki/Serial\_port\]\](https://en.wikipedia.org/wiki/Serial_port]\)\]

```cpp
Serial pc\(bblabla\);
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

# Task management APIs

## RTOS

Real Time Operating System based on Keil RTX code. See following RTOS section.

## Event loop

Postpone the execution of a code sequence from an interrupt hander to user or different context.

## Ticker

Calls a function repeatedly and at a specified rate

```cpp
Ticker ticker;
```

## Time

Date and time manipulation functions.  Support for time acquisition, conversion between date formats and formatted output to strings.

## Timeout

Set up an interrupt to call a function after a specified delay

```cpp
Timeout timeout;
```

## Timer

Create, start, stop and read a timer for measuring small times \(between microseconds and seconds\)

```cpp
Timer timer;
```

## Wait

Simple wait capabilities¨

```cpp
Example
```

# RTOS basics

## Thread

Defining, creating and controlling thread functions in the system.

```cpp
Thread t;
```

## Mutex

Synchronize execution of threads, for example to protect access to a shared resource.

```cpp
Mutex mutex;
```

## Semaphore

Manages thread access to a pool of shared resources of a certain type.

```cpp
Semaphore semaphore;
```

## Signals

Each Thread can wait for signals and to be notified of events.

```cpp
Signal
```

## Queue

Allows queue pointers to data from producer threads to consumer threads.

```cpp
Queue
```

## MemoryPool

Define and manage fixed-size memory pools.

```cpp
MemoryPool
```

## Mail

Like queue, with the added benefit of providing a memory pool for allocating messages.

```cpp
Mail
```

## Interrupts

The same RTOS API can be used in ISR.  See InterruptIn reference.

Warnings

* Cannot use mutex in ISR.
* Wait in ISR is not allowed.



