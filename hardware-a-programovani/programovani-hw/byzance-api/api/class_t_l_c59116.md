---
search:
    keywords: ['TLC59116', 'TLC59116', 'initialize', 'reset_sw', 'set_channel', 'set_all_channels', 'set_register', 'set_global_pwm']
---

# class TLC59116

Class to control **[TLC59116](class_t_l_c59116.md)** 16-channel 8-bit I2C PWM driver. 
## Public Functions

|Type|Name|
|-----|-----|
||[**TLC59116**](class_t_l_c59116.md#1aecffe9e8118ccc05387f873a4595e9fb) () |
|uint8\_t|[**initialize**](class_t_l_c59116.md#1a145f6d6184110ae195d7136be5552815) (PinName sda, PinName scl) |
|uint8\_t|[**reset\_sw**](class_t_l_c59116.md#1a97b32e9dd79c5d8a386877ffb74795ca) (void) |
|uint8\_t|[**set\_channel**](class_t_l_c59116.md#1a13cfd68eae78cb868bf24ec63c299618) (uint8\_t channel, uint8\_t pwm) |
|uint8\_t|[**set\_all\_channels**](class_t_l_c59116.md#1ad5024f365a00d27adf56a3d3e13ffd8b) (uint8\_t \* data) |
|uint8\_t|[**set\_register**](class_t_l_c59116.md#1a0caff956aef1390e6bc5745d81495204) (uint8\_t reg, uint8\_t value) |
|uint8\_t|[**set\_global\_pwm**](class_t_l_c59116.md#1a1ce8715db0b58cec11e484aaff22c44a) (uint8\_t pwm) |


## Public Functions Documentation

### function <a id="1aecffe9e8118ccc05387f873a4595e9fb" href="#1aecffe9e8118ccc05387f873a4595e9fb">TLC59116</a>

```cpp
TLC59116::TLC59116 ()
```


**[TLC59116](class_t_l_c59116.md)** driver constructor. 

### function <a id="1a145f6d6184110ae195d7136be5552815" href="#1a145f6d6184110ae195d7136be5552815">initialize</a>

```cpp
uint8_t TLC59116::initialize (
    PinName sda,
    PinName scl
)
```


Initialization of the **[TLC59116](class_t_l_c59116.md)** driver and configuration to default state, i.e. all outputs anabled, individual and global PWM active.


**Returns:**

Return 0 if success. Non zero value means some error. 




### function <a id="1a97b32e9dd79c5d8a386877ffb74795ca" href="#1a97b32e9dd79c5d8a386877ffb74795ca">reset\_sw</a>

```cpp
uint8_t TLC59116::reset_sw (
    void 
)
```


Reset the **[TLC59116](class_t_l_c59116.md)** chip to power on state (good to call "initialize" function to get it work). 

### function <a id="1a13cfd68eae78cb868bf24ec63c299618" href="#1a13cfd68eae78cb868bf24ec63c299618">set\_channel</a>

```cpp
uint8_t TLC59116::set_channel (
    uint8_t channel,
    uint8_t pwm
)
```


Set single channel output number "channel" with given PWM value.


**Parameters:**


* _channel_ Numbers 0 to 15 (16 channels). 
* _pwm_ Value from 0 (off) to 255 (fully on). 



**Returns:**

Return 0 if success. Non zero value means some error. 




### function <a id="1ad5024f365a00d27adf56a3d3e13ffd8b" href="#1ad5024f365a00d27adf56a3d3e13ffd8b">set\_all\_channels</a>

```cpp
uint8_t TLC59116::set_all_channels (
    uint8_t * data
)
```


Set all 16 channels with one command with given PWM values.


**Parameters:**


* _data_ Array with 16 uint8\_t items with PWM value (array element 0 = channel 0, etc). 



**Returns:**

Return 0 if success. Non zero value means some error. 




### function <a id="1a0caff956aef1390e6bc5745d81495204" href="#1a0caff956aef1390e6bc5745d81495204">set\_register</a>

```cpp
uint8_t TLC59116::set_register (
    uint8_t reg,
    uint8_t value
)
```


Direct write to single register in the **[TLC59116](class_t_l_c59116.md)**. Can be used to get the device to alternative configuration.


**Parameters:**


* _reg_ See this header file with register definitions. 



**Returns:**

Return 0 if success. Non zero value means some error. 




### function <a id="1a1ce8715db0b58cec11e484aaff22c44a" href="#1a1ce8715db0b58cec11e484aaff22c44a">set\_global\_pwm</a>

```cpp
uint8_t TLC59116::set_global_pwm (
    uint8_t pwm
)
```


Default configuration also use global outputs dimming. Each output has individual (256 steps) and global dimming (256 steps) ability.


**Parameters:**


* _pwm_ Value from 0 (off) to 255 (fully on). 



**Returns:**

Return 0 if success. Non zero value means some error. 






----------------------------------------
The documentation for this class was generated from the following file: `D:/w/hw-libs/\_libs\_/libraries/TLC59116.h`
