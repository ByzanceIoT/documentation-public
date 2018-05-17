# Časování

## Ticker

Umožňuje periodické volání funkcí s mikrosekundovou přesností.

```cpp
#include "byzance.h"
Ticker ticker;
DigitalOut led(LED_BLUE);
​
void flip() {    
    led = !led;    //blue led is blinking
}
​
void init(){
    Byzance::led_module(false);  //disable LED module for Byzance
    ticker.attach(&flip,2.0);    //call funciton flip every 2 seconds
}
​
void loop(){
    printf("im running\n");
    Thread::wait(1000);
}
```

## Timeout

Umožňuje zpožděné volání příslušné funkce s mikrosekundovou přesností.

```cpp
#include "byzance.h"
Timeout timeout;
DigitalOut led(LED_BLUE);    //led control is inverted

void turn_off() {    
    led = 1;    //turn off blue led
}

void init(){
    Byzance::led_module(false);      //disable LED module for Byzance
    led = 0;                         //turn on blue led
    timeout.attach(&turn_off,2.0);    //call funciton turn_off after 2 seconds
}

void loop(){
    printf("im running\n");
    Thread::wait(1000);
}
```

## Timer

Umožňuje měření časových úseků až s mikrosekundovou přesností. 

```cpp
#include "byzance.h"

DigitalOut led(LED_BLUE);
Timer timer;

void init(){
    Byzance::led_module(false);      //disable LED module for Byzance
    timer.start();                   //start the timer
}

void loop(){
    if(timer.read_ms() > 2000){    //if timer exceedes 2000ms
        timer.stop();    //stop the timer
        timer.reset();   //reset the timer to zero
        led = !led;      //flip the LED
        timer.start();   //and start timer again
    }
    Thread::wait(50);
}
```

## Wait

Simple wait capabilities

```cpp
Example
```

