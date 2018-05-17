# RTOS

## Thread

Defining, creating and controlling thread functions in the system.

```cpp
#include "byzance.h"

DigitalOut led(LED_BLUE);
Thread thread;

void led_thread() {
    while (true) {	//loop the thread
        led = !led;	//flip blue led
        Thread::wait(1000);	//wait for a second
    }
}

void init() {
	Byzance::led_module(false);  //disable LED module for Byzance
    thread.start(led_thread);	 //start the thread
}

void loop(){
    printf("i do nothing\n");	//main thread does actually nothing
    Thread::wait(500);
}
```

## Mutex

Synchronize execution of threads, for example to protect access to a shared resource.

```cpp
#include "byzance.h"

DigitalOut led(LED_BLUE);
Thread thread;
Mutex led_protection;	//led access protection

void led_thread() {
    while (true) {	//loop the thread
    	led_protection.lock();	//lock or wait forever for unlock
    	for(uint8_t i=0; i<10; i++){	//blink 10 times fast
			led = 1;	//flip blue led
			Thread::wait(50);
			led = 0;
			Thread::wait(50);
    	}
    	led_protection.unlock();
    }
}

void init() {
	Byzance::led_module(false);  //disable LED module for Byzance
    thread.start(led_thread);	 //start the thread
}

void loop(){
	led_protection.lock();	//lock or wait forever for unlock
	for(uint8_t i=0; i<10; i++){	//blink 5 times slow
		led = 1;	//flip blue led
		Thread::wait(200);	//wait for a second
		led = 0;
		Thread::wait(200);
	}
	led_protection.unlock();
}
```

## Semaphore

Manages thread access to a pool of shared resources of a certain type.

```cpp
Semaphore semaphore;
```

## Signals

Each Thread can wait for signals and to be notified of events.

```cpp
#include "byzance.h"

#define BLINK_SIGNAL 0x01

DigitalOut led(LED_BLUE);
Thread thread;

void led_thread() {
    while (true) {	//loop the thread
    	osEvent event = Thread::signal_wait(0);	//wait for any signal forever
    	if(event.status == osEventSignal && (event.value.signals & BLINK_SIGNAL)){	//if event was signal and signal is BLINK_SIGNAL
			for(uint8_t i=0; i<10; i++){	//blink 10 times fast
				led = 0;
				Thread::wait(50);
				led = 1;
				Thread::wait(50);
			}
    	}
    }
}

void init() {
	Byzance::led_module(false);  //disable LED module for Byzance
    thread.start(led_thread);	 //start the thread
}

void loop(){	//set signal for thread once in 5 seconds
	thread.signal_set(BLINK_SIGNAL);	//set signal for thread
	Thread::wait(5000);					//wait for 5s
}
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

