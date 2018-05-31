---
search:
  keywords:
    - I2CWrapper
    - _address
    - I2CWrapper
    - write_reg
    - write_reg
    - read_reg
    - read_reg
    - write_bit
    - read_bit
    - search
---

# I2CWrapper

Class that helps communicating over I2C.

Inherits the following classes: **I2C**

## Protected Attributes

| Type | Name |
| --- | --- |
| uint8\_t | [**\_address**](i2cwrapper.md#1a1f91e51cd8fdd06bf5512d379d49465b) |

## Public Functions

| Type | Name |
| --- | --- |
|  | [**I2CWrapper**](i2cwrapper.md#1a3d5c32611b4a9ca539cfcb48ce1cc3dc) \(PinName sda, PinName scl, uint8\_t address\) |
| int | [**write\_reg**](i2cwrapper.md#1a818a5c98cd8d38d2614e811c8c28c8e3) \(uint8\_t reg, uint8\_t val\) |
| int | [**write\_reg**](i2cwrapper.md#1ad50b3a8b13526dadf24f2fa3c78fc5d9) \(uint8\_t reg, uint8\_t \* val, uint16\_t size\) |
| int | [**read\_reg**](i2cwrapper.md#1a44ee5857e4b3bf043a2c49e87c65d8a3) \(uint8\_t reg, uint8\_t \* val\) |
| int | [**read\_reg**](i2cwrapper.md#1a58716c6f82093a3bb6ab14c0d1224aec) \(uint8\_t reg, uint8\_t \* val, uint16\_t size\) |
| int | [**write\_bit**](i2cwrapper.md#1a0cf56e57f383de425b9e586dd067e279) \(uint8\_t reg, uint8\_t bit, bool val\) |
| int | [**read\_bit**](i2cwrapper.md#1a094e735dbcc202f1ac03ff602d576345) \(uint8\_t reg, uint8\_t bit, bool \* val\) |
| int | [**search**](i2cwrapper.md#1ac1d265634a985bf2e3cc337bef22043d) \(\) |

## Protected Attributes Documentation

### variable [\_address](i2cwrapper.md#1a1f91e51cd8fdd06bf5512d379d49465b)

```cpp
uint8_t I2CWrapper::_address;
```

## Public Functions Documentation

### function [I2CWrapper](i2cwrapper.md#1a3d5c32611b4a9ca539cfcb48ce1cc3dc)

```cpp
I2CWrapper::I2CWrapper (
    PinName sda,
    PinName scl,
    uint8_t address
)
```

[**I2CWrapper**](i2cwrapper.md) constructor

**Parameters:**

* _sda_ I2C SDA pin 
* _scl_ I2C SCL pin 
* _address_ I2C address of device

**Returns:**

0 on success, non-0 on fail

### function [write\_reg](i2cwrapper.md#1a818a5c98cd8d38d2614e811c8c28c8e3)

```cpp
int I2CWrapper::write_reg (
    uint8_t reg,
    uint8_t val
)
```

Write value to register.

**Parameters:**

* _reg_ register to write in 
* _val_ value to write

**Returns:**

0 on success, non-0 on fail

### function [write\_reg](i2cwrapper.md#1ad50b3a8b13526dadf24f2fa3c78fc5d9)

```cpp
int I2CWrapper::write_reg (
    uint8_t reg,
    uint8_t * val,
    uint16_t size
)
```

Write multiple values to registers.

**Parameters:**

* _reg_ device register to start from 
* _val_ pointer to array with values to write 
* _size_ number of bytes to write

**Returns:**

0 on success, non-0 on fail

### function [read\_reg](i2cwrapper.md#1a44ee5857e4b3bf043a2c49e87c65d8a3)

```cpp
int I2CWrapper::read_reg (
    uint8_t reg,
    uint8_t * val
)
```

Read register.

**Parameters:**

* _reg_ register to read 
* _val_ pointer to the byte to read data in to

**Returns:**

0 on success, non-0 on fail

### function [read\_reg](i2cwrapper.md#1a58716c6f82093a3bb6ab14c0d1224aec)

```cpp
int I2CWrapper::read_reg (
    uint8_t reg,
    uint8_t * val,
    uint16_t size
)
```

Read multiple registers.

**Parameters:**

* _reg_ register to start reading from 
* _val_ pointer to the byte array to read data in to 
* _size_ mumber of bytes to read

**Returns:**

0 on success, non-0 on fail

### function [write\_bit](i2cwrapper.md#1a0cf56e57f383de425b9e586dd067e279)

```cpp
int I2CWrapper::write_bit (
    uint8_t reg,
    uint8_t bit,
    bool val
)
```

Write bit of the register.

**Parameters:**

* _reg_ register to write in 
* _bit_ bit to write \(0 - 7\) 
* _val_ value to write \(1/0\)

**Returns:**

0 on success, non-0 on fail

### function [read\_bit](i2cwrapper.md#1a094e735dbcc202f1ac03ff602d576345)

```cpp
int I2CWrapper::read_bit (
    uint8_t reg,
    uint8_t bit,
    bool * val
)
```

Read bit of the register

**Parameters:**

* _reg_ register to read from 
* _bit_ bit to read \(0 - 7\) 
* _\*val_ pointer to the bit to read data in

**Returns:**

0 on success, non-0 on fail

### function [search](i2cwrapper.md#1ac1d265634a985bf2e3cc337bef22043d)

```cpp
int I2CWrapper::search ()
```

Try all addresses on I2C bus and print results to stdio.

The documentation for this class was generated from the following file: `D:/w/hw-libs/\_libs\_/libraries/I2CWrapper.h`

