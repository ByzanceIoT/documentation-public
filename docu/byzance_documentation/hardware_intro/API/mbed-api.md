# MBED API

MBED je open-source operační systém a sada knihoven vyvíjených konsorciem ARM. Je možné jej stáhnout [z Githubu](https://github.com/ARMmbed/mbed-os). Byzance k MBED přidává vlastní targety, definici pinů a nad MBED běží další služby v mikrokontroléru, které se starají o aktualizaci firmware a komunikaci se servery. Součástí MBED jsou knihovny pro BLE, LWIP, mbedTLS, nanostack a další.

Dokumentace k nejnovějšímu API je dostupná [na webu projektu](https://docs.mbed.com/docs/mbed-os-api-reference/en/latest/).



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



