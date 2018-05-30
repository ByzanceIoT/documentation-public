---
search:
    keywords: ['Servo', '_pwm', '_range', '_degrees', '_p', 'Servo', 'write', 'read', 'position', 'calibrate', 'operator=', 'operator=', 'operator float']
---

# class Servo

Driver for PWM controlled servo motors. [More...](#detailed-description)
## Protected Attributes

|Type|Name|
|-----|-----|
|PwmOut|[**\_pwm**](class_servo.md#1af786610974ae4db9d34e34f0044f1e22)|
|float|[**\_range**](class_servo.md#1af9ae8d8b2a1b5a3a41a9cc8bfa8f86aa)|
|float|[**\_degrees**](class_servo.md#1a674c5f736156204c478a5d3b1b44f708)|
|float|[**\_p**](class_servo.md#1a68b6fe7d0853c211280cb914fbb341dd)|


## Public Functions

|Type|Name|
|-----|-----|
||[**Servo**](class_servo.md#1a9f6bdad36dd357a385e0f5e3f8ce1a35) (PinName pin) |
|void|[**write**](class_servo.md#1a2c508614c398623245e227831c45ed83) (float percent) |
|float|[**read**](class_servo.md#1afa40011959b6addcfeaa93e526fa3427) () |
|void|[**position**](class_servo.md#1a6d764ad653c7c1c89c8085e881cd7e76) (float degrees) |
|void|[**calibrate**](class_servo.md#1a46f7f77f718cba3cee94ddfe6436bd75) (float range = 0.0005, float degrees = 45.0) |
|**[Servo](class_servo.md)** &|[**operator=**](class_servo.md#1ab6b972f5ab16c19a61dbd94743e5103b) (float percent) |
|**[Servo](class_servo.md)** &|[**operator=**](class_servo.md#1a65139bbecf0856b2dd4e18d61d834a16) (**[Servo](class_servo.md)** & rhs) |
||[**operator float**](class_servo.md#1a412272601a695f8a43f50a3a6f22dd39) () |


## Detailed Description

**[Servo](class_servo.md)** control class, based on a PwmOut
Example: 
```cpp
// Continuously sweep the servo through it's full range
#include "mbed.h"
#include "Servo.h"

Servo myservo(p21);

int main() {
    while(1) {
        for(int i=0; i<100; i++) {
            myservo = i/100.0;
            wait(0.01);
        }
        for(int i=100; i>0; i--) {
            myservo = i/100.0;
            wait(0.01);
        }
    }
}
```

 
## Protected Attributes Documentation

### variable <a id="1af786610974ae4db9d34e34f0044f1e22" href="#1af786610974ae4db9d34e34f0044f1e22">\_pwm</a>

```cpp
PwmOut Servo::_pwm;
```



### variable <a id="1af9ae8d8b2a1b5a3a41a9cc8bfa8f86aa" href="#1af9ae8d8b2a1b5a3a41a9cc8bfa8f86aa">\_range</a>

```cpp
float Servo::_range;
```



### variable <a id="1a674c5f736156204c478a5d3b1b44f708" href="#1a674c5f736156204c478a5d3b1b44f708">\_degrees</a>

```cpp
float Servo::_degrees;
```



### variable <a id="1a68b6fe7d0853c211280cb914fbb341dd" href="#1a68b6fe7d0853c211280cb914fbb341dd">\_p</a>

```cpp
float Servo::_p;
```



## Public Functions Documentation

### function <a id="1a9f6bdad36dd357a385e0f5e3f8ce1a35" href="#1a9f6bdad36dd357a385e0f5e3f8ce1a35">Servo</a>

```cpp
Servo::Servo (
    PinName pin
)
```


Create a servo object connected to the specified PwmOut pin


**Parameters:**


* _pin_ PwmOut pin to connect to 



### function <a id="1a2c508614c398623245e227831c45ed83" href="#1a2c508614c398623245e227831c45ed83">write</a>

```cpp
void Servo::write (
    float percent
)
```


Set the servo position, normalised to it's full range


**Parameters:**


* _percent_ A normalised number 0.0-1.0 to represent the full range. 



### function <a id="1afa40011959b6addcfeaa93e526fa3427" href="#1afa40011959b6addcfeaa93e526fa3427">read</a>

```cpp
float Servo::read ()
```


Read the servo motors current position


**Parameters:**


* _returns_ A normalised number 0.0-1.0 representing the full range. 



### function <a id="1a6d764ad653c7c1c89c8085e881cd7e76" href="#1a6d764ad653c7c1c89c8085e881cd7e76">position</a>

```cpp
void Servo::position (
    float degrees
)
```


Set the servo position


**Parameters:**


* _degrees_ **[Servo](class_servo.md)** position in degrees 



### function <a id="1a46f7f77f718cba3cee94ddfe6436bd75" href="#1a46f7f77f718cba3cee94ddfe6436bd75">calibrate</a>

```cpp
void Servo::calibrate (
    float range = 0.0005,
    float degrees = 45.0
)
```


Allows calibration of the range and angles for a particular servo


**Parameters:**


* _range_ Pulsewidth range from center (1.5ms) to maximum/minimum position in seconds 
* _degrees_ Angle from centre to maximum/minimum position in degrees 



### function <a id="1ab6b972f5ab16c19a61dbd94743e5103b" href="#1ab6b972f5ab16c19a61dbd94743e5103b">operator=</a>

```cpp
Servo & Servo::operator= (
    float percent
)
```


Shorthand for the write and read functions 

### function <a id="1a65139bbecf0856b2dd4e18d61d834a16" href="#1a65139bbecf0856b2dd4e18d61d834a16">operator=</a>

```cpp
Servo & Servo::operator= (
    Servo & rhs
)
```



### function <a id="1a412272601a695f8a43f50a3a6f22dd39" href="#1a412272601a695f8a43f50a3a6f22dd39">operator float</a>

```cpp
Servo::operator float ()
```





----------------------------------------
The documentation for this class was generated from the following file: `D:/w/hw-libs/\_libs\_/libraries/Servo.h`
