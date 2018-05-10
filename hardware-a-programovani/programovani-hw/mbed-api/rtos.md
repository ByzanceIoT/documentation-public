# RTOS

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

The same RTOS API can be used in ISR. See InterruptIn reference.

Warnings

* Cannot use mutex in ISR.
* Wait in ISR is not allowed.

