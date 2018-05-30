---
search:
    keywords: ['WakeUp', 'set', 'set_ms', 'attach', 'calibrate']
---

# class WakeUp

Class to make wake up a microcontroller from deepsleep using a low-power timer. [More...](#detailed-description)
## Public Static Functions

|Type|Name|
|-----|-----|
|static void|[**set**](class_wake_up.md#1a35555135d939991c9b288c7fdf2acf1e) (uint32\_t s) |
|static void|[**set\_ms**](class_wake_up.md#1abd46caf0490902d7330e5847cd0807fc) (uint32\_t ms) |
|static void|[**attach**](class_wake_up.md#1a2acb127a35ced9e6d2c5d8013db7de66) (Callback< void()> function) |
|static void|[**calibrate**](class_wake_up.md#1a27d093534db639951961f3f8c7fe4fa7) (void) |


## Detailed Description

Class to make wake up a microcontroller from deepsleep using a low-power timer.

```cpp
// Depending on the LED connections either the LED is off the 2 seconds
// the target spends in deepsleep(), and on for the other second. Or it is inverted 

#include "mbed.h"
#include "WakeUp.h"

DigitalOut myled(LED1);

int main() {
    wait(5);

    //The low-power oscillator can be quite inaccurate on some targets
    //this function calibrates it against the main clock
    WakeUp::calibrate();
   
    while(1) {
        //Set LED to zero
        myled = 0;
        
        //Set wakeup time for 2 seconds
        WakeUp::set_ms(2000);
        
        //Enter deepsleep, the program won't go beyond this point until it is woken up
        deepsleep();
        
        //Set LED for 1 second to one
        myled = 1;
        wait(1);
    }
}
```

 
## Public Static Functions Documentation

### function <a id="1a35555135d939991c9b288c7fdf2acf1e" href="#1a35555135d939991c9b288c7fdf2acf1e">set</a>

```cpp
static void WakeUp::set (
    uint32_t s
)
```


Set the timeout


**Parameters:**


* _s_ required time in seconds 



### function <a id="1abd46caf0490902d7330e5847cd0807fc" href="#1abd46caf0490902d7330e5847cd0807fc">set\_ms</a>

```cpp
static void WakeUp::set_ms (
    uint32_t ms
)
```


Set the timeout


**Parameters:**


* _ms_ required time in milliseconds 



### function <a id="1a2acb127a35ced9e6d2c5d8013db7de66" href="#1a2acb127a35ced9e6d2c5d8013db7de66">attach</a>

```cpp
static void WakeUp::attach (
    Callback< void()> function
)
```


Attach a function to be called after timeout
This is optional, if you just want to wake up you do not need to attach a function.
Important: Many targets will run the wake-up routine at reduced clock speed, afterwards clock speed is restored. This means that clock speed dependent functions, such as printf might end up distorted.

```cpp
// Attaching regular function
WakeUp::attach(&yourFunc);
// Attaching member function inside another library    
WakeUp::attach(callback(this, &YourLib::yourLibFunction));    
```


It uses the new Callback system to attach functions.


**Parameters:**


* _\*function_ function to call 



### function <a id="1a27d093534db639951961f3f8c7fe4fa7" href="#1a27d093534db639951961f3f8c7fe4fa7">calibrate</a>

```cpp
static void WakeUp::calibrate (
    void 
)
```


Calibrate the timer
Some of the low-power timers have very bad accuracy. This function calibrates it against the main timer.
Warning: Blocks for 100ms! 



----------------------------------------
The documentation for this class was generated from the following file: `D:/w/hw-libs/\_libs\_/libraries/WakeUp.h`
