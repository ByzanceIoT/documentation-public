===== MBED =====

MBED je open-source operační systém a sada knihoven vyvíjených konsorciem ARM. Je možné jej stáhnout \[\[[https://github.com/ARMmbed/mbed-os\|Githubu\]\](https://github.com/ARMmbed/mbed-os|Githubu]\)\]. Byzance k MBED přidává vlastní targety, definici pinů a nad MBED běží další služby v mikrokontroléru, které se starají o aktualizaci firmware a komunikaci se servery. Součástí MBED jsou knihovny pro BLE, LWIP, mbedTLS, nanostack a další.

Dokumentace k nejnovějšímu API je dostupná na webu \[\[[https://docs.mbed.com/docs/mbed-os-api-reference/en/latest/\]\](https://docs.mbed.com/docs/mbed-os-api-reference/en/latest/]\)\]

==== Vstupně/výstupní API ====

=== AnalogIn ===

Read an external voltage applied to an analog input pin.

```
AnalogIn ain\(pin\_name\);

printf\(”ain value = %3.3f%%\n”, ain.read\(\)\);
```

=== AnalogOut ===

Set the voltage of an analog output pin in the range of VSS to VCC.

&lt;code&gt;

```
AnalogOut aout\(pin\_name\);

aout.write\(some\_float\);
```

&lt;/code&gt;

=== DigitalIn ===

Read the value of an digital input pin

&lt;code&gt;

```
DigitalIn din\(pin\_name\);

printf\("pin has value : %d \n", din.read\(\)\);
```

&lt;/code&gt;

=== DigitalOut ===

Configure and control a digital output pin

&lt;code&gt;

```
DigitalOut dout\(pin\_name\);

dout=1;
```

&lt;/code&gt;

=== DigitalInOut ===

Bidirectional digital pin, combination of DigitalIn and DigitalOut

&lt;code&gt;

```
DigitalInOut diout\(pin\_name\);

diout.output\(\);

diout = 1;

diout.input\(\);

pc.printf\("diout value = %d \n", diout.read\(\)\);
```

&lt;/code&gt;

=== BusIn ===

Number of DigitalIn pins that can be read as one value.

&lt;code&gt;

```
BusIn    
```

&lt;/code&gt;

=== BusOut ===

Number of DigitalOut pins that can be written as one value.

&lt;code&gt;

```
BusOut
```

&lt;/code&gt;

=== BusInOut ===

Number of DigitalInOut pins that can be read and written as one value.

&lt;code&gt;

```
BusInOut
```

&lt;/code&gt;

=== PortIn ===

Similar to BusIn, much faster but much less flexible.

&lt;code&gt;

```
PortIn
```

&lt;/code&gt;

=== PortOut ===

Similar to BusOut, much faster but much less flexible.

&lt;code&gt;

```
PortOut
```

&lt;/code&gt;

=== PortInOut ===

Similar to BusInOut, much faster but much less flexible.

&lt;code&gt;

```
PortInOut
```

&lt;/code&gt;

=== PwmOut ===

Interface to control the frequency and mark-to-space ration of digital pulse train.

&lt;code&gt;

```
PwmOut
```

&lt;/code&gt;

=== InterruptIn ===

Trigger an event when a digital input pin changes.

&lt;code&gt;

```
InterruptIn
```

&lt;/code&gt;

==== Digital interface APIs ====

=== Serial ===

Generic serial protocol API, send and receive data.

See \[\[[https://en.wikipedia.org/wiki/Serial\_port\]\](https://en.wikipedia.org/wiki/Serial_port]\)\]

&lt;code&gt;

```
Serial pc\(bblabla\);
```

&lt;/code&gt;

=== SPI ===

Serial Peripheral Interface Master.

See [https://en.wikipedia.org/wiki/Serial\_Peripheral\_Interface\_Bus](https://en.wikipedia.org/wiki/Serial_Peripheral_Interface_Bus)

&lt;code&gt;

```
Example    
```

&lt;/code&gt;

=== SPISlave ===

Serial Peripheral Interface Slave.

&lt;code&gt;

```
SPISlave spislave;
```

&lt;/code&gt;

=== I2C ===

I2C Master functionality.

&lt;code&gt;

```
I2C i2c;
```

&lt;/code&gt;

=== I2CSlave ===

Use to communicate with I2C Master.

&lt;code&gt;

```
I2CSlave i2cslave;
```

&lt;/code&gt;

=== CAN ===

Controller-Area Network bus standard support.

&lt;code&gt;

```
CAN can;
```

&lt;/code&gt;

==== Task management APIs ====

=== RTOS ===

Real Time Operating System based on Keil RTX code. See following RTOS section.

=== Event loop ===

Postpone the execution of a code sequence from an interrupt hander to user or different context.

=== Ticker ===

Calls a function repeatedly and at a specified rate

&lt;code&gt;

Ticker ticker;

&lt;/code&gt;

=== Time ===

Date and time manipulation functions.  Support for time acquisition, conversion between date formats and formatted output to strings.

=== Timeout ===

Set up an interrupt to call a function after a specified delay

&lt;code&gt;

```
Timeout timeout;
```

&lt;/code&gt;

=== Timer ===

Create, start, stop and read a timer for measuring small times \(between microseconds and seconds\)

&lt;code&gt;

```
Timer timer;
```

&lt;/code&gt;

=== Wait ===

Simple wait capabilities¨

&lt;code&gt;

```
Example
```

&lt;/code&gt;

==== RTOS basics ====

Thread        Defining, creating and controlling thread functions in the system.

&lt;code&gt;

```
Thread thread;
```

&lt;/code&gt;

=== Mutex ===

Synchronize execution of threads, for example to protect access to a shared resource.

&lt;code&gt;

```
Mutex mutex;
```

&lt;/code&gt;

=== Semaphore ===

Manages thread access to a pool of shared resources of a certain type.

&lt;code&gt;

```
Semaphore semaphore;
```

&lt;/code&gt;

=== Signals ===

Each Thread can wait for signals and to be notified of events.

&lt;code&gt;

```
Signal
```

&lt;/code&gt;

=== Queue ===

Allows queue pointers to data from producer threads to consumer threads.

&lt;code&gt;

```
Queue
```

&lt;/code&gt;

=== MemoryPool ===

Define and manage fixed-size memory pools.

&lt;code&gt;

```
MemoryPool
```

&lt;/code&gt;

=== Mail ===

Like queue, with the added benefit of providing a memory pool for allocating messages.

&lt;code&gt;

```
Mail
```

&lt;/code&gt;

=== Interrupts ===

The same RTOS API can be used in ISR.  See InterruptIn reference.

Warnings

\* Cannot use mutex in ISR.

\* Wait in ISR is not allowed.

