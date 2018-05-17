# RTOS

## [Thread](https://os.mbed.com/docs/latest/reference/thread.html)

Defining, creating and controlling thread functions in the system.

```cpp
#include "byzance.h"

Serial pc(SERIAL_TX, SERIAL_RX);	//USBSerial pc(0x1f00, 0x2012, 0x0001, false);
DigitalOut led(LED_BLUE);
Thread thread;

void led_thread() {
    while (true) {    //loop the thread
        led = !led;    //flip blue led
        Thread::wait(1000);    //wait for a second
    }
}

void init() {
    Byzance::led_module(false);  //disable LED module for Byzance
    thread.start(led_thread);     //start the thread
}

void loop(){
    pc.printf("i do nothing\n");    //main thread does actually nothing
    Thread::wait(500);
}
```

## [Mutex](https://os.mbed.com/docs/latest/reference/mutex.html)

Synchronize execution of threads, for example to protect access to a shared resource.

```cpp
#include "byzance.h"

Serial pc(SERIAL_TX, SERIAL_RX);	//USBSerial pc(0x1f00, 0x2012, 0x0001, false);
DigitalOut led(LED_BLUE);
Thread thread;
Mutex led_protection;    //led access protection

void led_thread() {
    while (true) {    //loop the thread
        led_protection.lock();    //lock or wait forever for unlock
        for(uint8_t i=0; i<10; i++){    //blink 10 times fast
            led = 1;    //flip blue led
            Thread::wait(50);
            led = 0;
            Thread::wait(50);
        }
        led_protection.unlock();
    }
}

void init() {
    Byzance::led_module(false);  //disable LED module for Byzance
    thread.start(led_thread);     //start the thread
}

void loop(){
    led_protection.lock();    //lock or wait forever for unlock
    for(uint8_t i=0; i<10; i++){    //blink 5 times slow
        led = 1; 
        Thread::wait(200); 
        led = 0;
        Thread::wait(200);
    }
    led_protection.unlock();
}
```

## [Semaphore](https://os.mbed.com/docs/latest/reference/semaphore.html)

Manages thread access to a pool of shared resources of a certain type.

```cpp
Semaphore semaphore;
```

## Signals

Each Thread can wait for signals and to be notified of events.

```cpp
#include "byzance.h"

#define BLINK_SIGNAL 0x01

Serial pc(SERIAL_TX, SERIAL_RX);	//USBSerial pc(0x1f00, 0x2012, 0x0001, false);
DigitalOut led(LED_BLUE);
Thread thread;

void led_thread() {
    while (true) {    //loop the thread
        osEvent event = Thread::signal_wait(0);    //wait for any signal forever
        if(event.status == osEventSignal && (event.value.signals & BLINK_SIGNAL)){    //if event was signal and signal is BLINK_SIGNAL
            for(uint8_t i=0; i<10; i++){    //blink 10 times fast
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
    thread.start(led_thread);     //start the thread
}

void loop(){    //set signal for thread once in 5 seconds
    thread.signal_set(BLINK_SIGNAL);
    Thread::wait(5000);
}
```

## [Queue](https://os.mbed.com/docs/latest/reference/queue.html)

Allows queue pointers to data from producer threads to consumer threads.

```cpp
#include "byzance.h"

Serial pc(SERIAL_TX, SERIAL_RX);	//USBSerial pc(0x1f00, 0x2012, 0x0001, false);
DigitalOut led(LED_BLUE);
InterruptIn button(USR);
Queue<void, 16> queue;	//maximum is 16 records, no data type delivered

void button_pressed(){
	queue.put(0);	//on button pressed, add record to queue
}

void init() {
	Byzance::led_module(false);  //disable LED module for Byzance
    button.fall(&button_pressed);
}

//try to press button multiple times
void loop(){
	osEvent event = queue.get();	//wait for not empty queue forever
	static int pressed_times=0;
	if(event.status == osEventMessage){	//if event was osEventMessage
		pressed_times++;
		pc.printf("button pressed %d times\n",pressed_times);
		for(uint8_t i=0; i<10; i++){	//blink 10 times for each record in queue
			led = 0;
			Thread::wait(50);
			led = 1;
			Thread::wait(50);
		}
	}
}

```

## [MemoryPool](https://os.mbed.com/docs/latest/reference/memorypool.html)

Define and manage fixed-size memory pools.

```cpp
#include "byzance.h"

typedef struct {
    float    voltage;   /* AD result of measured voltage */
    float    current;   /* AD result of measured current */
    uint32_t counter;   /* A counter value               */
} message_t;

Serial pc(SERIAL_TX, SERIAL_RX);	//USBSerial pc(0x1f00, 0x2012, 0x0001, false);
MemoryPool<message_t, 16> mpool;
Queue<message_t, 16> queue;
Thread thread;

void send_thread (void) {
    uint32_t i = 0;
    while (true) {		//every 5 seconds queue 4 msgs
        for(uint8_t j = 0; j < 5; j++){
        	i++; // fake data update
			message_t *message = mpool.alloc();	//alloc memory for message
			message->voltage = (i * 0.1) * 33;
			message->current = (i * 0.1) * 11;
			message->counter = i;
			queue.put(message);		//queue the message
        }
        pc.printf("sent 4 msgs from send thread\n");
        Thread::wait(5000);
    }
}

void init(){
	thread.start(callback(send_thread));
}

void loop() {
	osEvent evt = queue.get();		//wait for not empty queue
	if (evt.status == osEventMessage) {
		message_t *message = (message_t*)evt.value.p;
		pc.printf("received msg no. %d voltage: %f V, current: %f A\n",message->counter, message->voltage, message->current);
		mpool.free(message);	//free msg from memory
	}

}
```

## [Mail](https://os.mbed.com/docs/latest/reference/mail.html)

Like queue, with the added benefit of providing a memory pool for allocating messages - combination of MemoryPool and Queue.

```cpp
#include "byzance.h"

typedef struct {
    float    voltage;   /* AD result of measured voltage */
    float    current;   /* AD result of measured current */
    uint32_t counter;   /* A counter value               */
} message_t;

Serial pc(SERIAL_TX, SERIAL_RX);	//USBSerial pc(0x1f00, 0x2012, 0x0001, false);
Mail<message_t, 16> mail_box;
Thread thread;

void send_thread (void) {
    uint32_t i = 0;
    while (true) {		//every 5 seconds queue 4 msgs
        for(uint8_t j = 0; j < 5; j++){
        	i++; // fake data update
			message_t *message = mail_box.alloc();	//alloc memory for message
			message->voltage = (i * 0.1) * 33;
			message->current = (i * 0.1) * 11;
			message->counter = i;
			mail_box.put(message);		//queue the message
        }
        pc.printf("sent 4 mails from send thread\n");
        Thread::wait(5000);
    }
}

void init(){
	thread.start(callback(send_thread));
}

void loop() {
	osEvent evt = mail_box.get();
	if (evt.status == osEventMail) {
		message_t *message = (message_t*)evt.value.p;
		pc.printf("received mail no. %d voltage: %f V, current: %f A\n",message->counter, message->voltage, message->current);
		mail_box.free(message);	//free msg from memory
	}
}
```

## Interrupts

The same RTOS API can be used in ISR. See InterruptIn reference.

Warnings

* Cannot use mutex in ISR.
* Wait in ISR is not allowed.

