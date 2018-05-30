---
search:
    keywords: ['PCA9536', '_i2c', 'PCA9536', 'set_all_inputs', 'set_all_outputs', 'set_output', 'set_input', 'set_value', 'set_value', 'get_value', 'get_value', '_write_reg', '_read_reg']
---

# class PCA9536

Driver for **[PCA9536](class_p_c_a9536.md)** 4-bit I2C IO pin expander. 
## Protected Attributes

|Type|Name|
|-----|-----|
|I2C|[**\_i2c**](class_p_c_a9536.md#1a8f15259f253fcbfec51bda4def6c3f0f)|


## Public Functions

|Type|Name|
|-----|-----|
||[**PCA9536**](class_p_c_a9536.md#1aa8c74423e4be02da4104b62580942606) (PinName sda, PinName scl) |
|int|[**set\_all\_inputs**](class_p_c_a9536.md#1ae4475825e0d9839b334dfaf75e768621) () |
|int|[**set\_all\_outputs**](class_p_c_a9536.md#1a00dc013e3d0c72c55826dac1676f0221) () |
|int|[**set\_output**](class_p_c_a9536.md#1af2b18413045efa0f9a054f4a1824edc7) (uint8\_t pin) |
|int|[**set\_input**](class_p_c_a9536.md#1aba6d6a1271cb21edff50ed62166ae34c) (uint8\_t pin) |
|int|[**set\_value**](class_p_c_a9536.md#1a3caea8b6b6c0c81d42923a2b40dee955) (uint8\_t value) |
|int|[**set\_value**](class_p_c_a9536.md#1af0772df4404dd3b9c508858586d3a4b6) (uint8\_t pin, uint8\_t value) |
|int|[**get\_value**](class_p_c_a9536.md#1ac4ef8af3a5a3c20212aa11675e8d643c) (uint8\_t \* value) |
|int|[**get\_value**](class_p_c_a9536.md#1ad8fa62739b1ba48fe53342a3d1967b07) (uint8\_t pin, uint8\_t \* value) |


## Protected Functions

|Type|Name|
|-----|-----|
|int|[**\_write\_reg**](class_p_c_a9536.md#1af3267c61f469ab6dbc0acc7e72acab14) (uint8\_t reg, uint8\_t val) |
|int|[**\_read\_reg**](class_p_c_a9536.md#1ac1c8abbb4c229db68dbd9a2d9797e2d9) (uint8\_t reg, uint8\_t \* val) |


## Protected Attributes Documentation

### variable <a id="1a8f15259f253fcbfec51bda4def6c3f0f" href="#1a8f15259f253fcbfec51bda4def6c3f0f">\_i2c</a>

```cpp
I2C PCA9536::_i2c;
```



## Public Functions Documentation

### function <a id="1aa8c74423e4be02da4104b62580942606" href="#1aa8c74423e4be02da4104b62580942606">PCA9536</a>

```cpp
PCA9536::PCA9536 (
    PinName sda,
    PinName scl
)
```



### function <a id="1ae4475825e0d9839b334dfaf75e768621" href="#1ae4475825e0d9839b334dfaf75e768621">set\_all\_inputs</a>

```cpp
int PCA9536::set_all_inputs ()
```


Set port as input.


**Returns:**

0 on success; non-0 on fail 




### function <a id="1a00dc013e3d0c72c55826dac1676f0221" href="#1a00dc013e3d0c72c55826dac1676f0221">set\_all\_outputs</a>

```cpp
int PCA9536::set_all_outputs ()
```


Set port as output.


**Returns:**

0 on success; non-0 on fail 




### function <a id="1af2b18413045efa0f9a054f4a1824edc7" href="#1af2b18413045efa0f9a054f4a1824edc7">set\_output</a>

```cpp
int PCA9536::set_output (
    uint8_t pin
)
```


Set pin as output.


**Parameters:**


* _pin_ pin number to set as output (0 - 3)



**Returns:**

0 on success; -2 on invalid pin; non-0 on fail 




### function <a id="1aba6d6a1271cb21edff50ed62166ae34c" href="#1aba6d6a1271cb21edff50ed62166ae34c">set\_input</a>

```cpp
int PCA9536::set_input (
    uint8_t pin
)
```


Set pin as input.


**Parameters:**


* _pin_ pin number to set (0 - 3)



**Returns:**

0 on success; -2 on invalid pin; non-0 on fail 




### function <a id="1a3caea8b6b6c0c81d42923a2b40dee955" href="#1a3caea8b6b6c0c81d42923a2b40dee955">set\_value</a>

```cpp
int PCA9536::set_value (
    uint8_t value
)
```


Set port value.


**Parameters:**


* _value_ value to set on port (0 - F)



**Returns:**

0 on success; non-0 on fail 




### function <a id="1af0772df4404dd3b9c508858586d3a4b6" href="#1af0772df4404dd3b9c508858586d3a4b6">set\_value</a>

```cpp
int PCA9536::set_value (
    uint8_t pin,
    uint8_t value
)
```


Set pin value.


**Parameters:**


* _pin_ pin number to set (0 - 3) 
* _pin_ value to set (0 or 1)



**Returns:**

0 on success; -2 on invalid pin; non-0 on fail 




### function <a id="1ac4ef8af3a5a3c20212aa11675e8d643c" href="#1ac4ef8af3a5a3c20212aa11675e8d643c">get\_value</a>

```cpp
int PCA9536::get_value (
    uint8_t * value
)
```


Get port value.


**Parameters:**


* _value_ pointer to byte to read the value in to



**Returns:**

0 on success; non-0 on fail 




### function <a id="1ad8fa62739b1ba48fe53342a3d1967b07" href="#1ad8fa62739b1ba48fe53342a3d1967b07">get\_value</a>

```cpp
int PCA9536::get_value (
    uint8_t pin,
    uint8_t * value
)
```


Get pin value.


**Parameters:**


* _pin_ pin to read 
* _value_ pointer to byte to read the value in to



**Returns:**

0 on success; -2 on invalid pin; non-0 on fail 




## Protected Functions Documentation

### function <a id="1af3267c61f469ab6dbc0acc7e72acab14" href="#1af3267c61f469ab6dbc0acc7e72acab14">\_write\_reg</a>

```cpp
int PCA9536::_write_reg (
    uint8_t reg,
    uint8_t val
)
```



### function <a id="1ac1c8abbb4c229db68dbd9a2d9797e2d9" href="#1ac1c8abbb4c229db68dbd9a2d9797e2d9">\_read\_reg</a>

```cpp
int PCA9536::_read_reg (
    uint8_t reg,
    uint8_t * val
)
```





----------------------------------------
The documentation for this class was generated from the following file: `D:/w/hw-libs/\_libs\_/libraries/PCA9536.h`
