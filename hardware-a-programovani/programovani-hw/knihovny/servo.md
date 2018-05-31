---
search:
  keywords:
    - Servo
    - _pwm
    - _range
    - _degrees
    - _p
    - Servo
    - write
    - read
    - position
    - calibrate
    - operator=
    - operator=
    - operator float
---

# Servo

Driver for PWM controlled servo motors. [More...](servo.md#detailed-description)

## Protected Attributes

| Type | Name |
| --- | --- |
| PwmOut | [**\_pwm**](servo.md#1af786610974ae4db9d34e34f0044f1e22) |
| float | [**\_range**](servo.md#1af9ae8d8b2a1b5a3a41a9cc8bfa8f86aa) |
| float | [**\_degrees**](servo.md#1a674c5f736156204c478a5d3b1b44f708) |
| float | [**\_p**](servo.md#1a68b6fe7d0853c211280cb914fbb341dd) |

## Public Functions

| Type | Name |
| --- | --- |
|  | [**Servo**](servo.md#1a9f6bdad36dd357a385e0f5e3f8ce1a35) \(PinName pin\) |
| void | [**write**](servo.md#1a2c508614c398623245e227831c45ed83) \(float percent\) |
| float | [**read**](servo.md#1afa40011959b6addcfeaa93e526fa3427) \(\) |
| void | [**position**](servo.md#1a6d764ad653c7c1c89c8085e881cd7e76) \(float degrees\) |
| void | [**calibrate**](servo.md#1a46f7f77f718cba3cee94ddfe6436bd75) \(float range = 0.0005, float degrees = 45.0\) |
| [**Servo**](servo.md) & | [**operator=**](servo.md#1ab6b972f5ab16c19a61dbd94743e5103b) \(float percent\) |
| [**Servo**](servo.md) & | [**operator=**](servo.md#1a65139bbecf0856b2dd4e18d61d834a16) \([**Servo**](servo.md) & rhs\) |
|  | [**operator float**](servo.md#1a412272601a695f8a43f50a3a6f22dd39) \(\) |

## Detailed Description

[**Servo**](servo.md) control class, based on a PwmOut Example:

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

### variable [\_pwm](servo.md#1af786610974ae4db9d34e34f0044f1e22)

```cpp
PwmOut Servo::_pwm;
```

### variable [\_range](servo.md#1af9ae8d8b2a1b5a3a41a9cc8bfa8f86aa)

```cpp
float Servo::_range;
```

### variable [\_degrees](servo.md#1a674c5f736156204c478a5d3b1b44f708)

```cpp
float Servo::_degrees;
```

### variable [\_p](servo.md#1a68b6fe7d0853c211280cb914fbb341dd)

```cpp
float Servo::_p;
```

## Public Functions Documentation

### function [Servo](servo.md#1a9f6bdad36dd357a385e0f5e3f8ce1a35)

```cpp
Servo::Servo (
    PinName pin
)
```

Create a servo object connected to the specified PwmOut pin

**Parameters:**

* _pin_ PwmOut pin to connect to 

### function [write](servo.md#1a2c508614c398623245e227831c45ed83)

```cpp
void Servo::write (
    float percent
)
```

Set the servo position, normalised to it's full range

**Parameters:**

* _percent_ A normalised number 0.0-1.0 to represent the full range. 

### function [read](servo.md#1afa40011959b6addcfeaa93e526fa3427)

```cpp
float Servo::read ()
```

Read the servo motors current position

**Parameters:**

* _returns_ A normalised number 0.0-1.0 representing the full range. 

### function [position](servo.md#1a6d764ad653c7c1c89c8085e881cd7e76)

```cpp
void Servo::position (
    float degrees
)
```

Set the servo position

**Parameters:**

* _degrees_ [**Servo**](servo.md) position in degrees 

### function [calibrate](servo.md#1a46f7f77f718cba3cee94ddfe6436bd75)

```cpp
void Servo::calibrate (
    float range = 0.0005,
    float degrees = 45.0
)
```

Allows calibration of the range and angles for a particular servo

**Parameters:**

* _range_ Pulsewidth range from center \(1.5ms\) to maximum/minimum position in seconds 
* _degrees_ Angle from centre to maximum/minimum position in degrees 

### function [operator=](servo.md#1ab6b972f5ab16c19a61dbd94743e5103b)

```cpp
Servo & Servo::operator= (
    float percent
)
```

Shorthand for the write and read functions

### function [operator=](servo.md#1a65139bbecf0856b2dd4e18d61d834a16)

```cpp
Servo & Servo::operator= (
    Servo & rhs
)
```

### function [operator float](servo.md#1a412272601a695f8a43f50a3a6f22dd39)

```cpp
Servo::operator float ()
```

The documentation for this class was generated from the following file: `D:/w/hw-libs/\_libs\_/libraries/Servo.h`

