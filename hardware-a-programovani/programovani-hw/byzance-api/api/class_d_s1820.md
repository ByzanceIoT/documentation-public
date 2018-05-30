---
search:
    keywords: ['DS1820', 'DS1820', 'DS1820', 'begin', 'isPresent', 'setResolution', 'startConversion', 'read', 'read']
---

# class DS1820

Driver to control **[DS1820](class_d_s1820.md)** 1-Wire temperature sensor. 
## Public Functions

|Type|Name|
|-----|-----|
||[**DS1820**](class_d_s1820.md#1a701b51269a6af8ccb319ea5f1eda2686) (PinName pin) <br>Constructs a generic **[DS1820](class_d_s1820.md)** sensor. |
||[**DS1820**](class_d_s1820.md#1a3b0b002ab8834b64b0f20852a55b80af) (char model, PinName pin) <br>Constructs a specific model. |
|bool|[**begin**](class_d_s1820.md#1a1fc30caa0df9ffb740cfd7e7956f4f8d) (void) <br>Detects and initializes the actual **[DS1820](class_d_s1820.md)** model. |
|bool|[**isPresent**](class_d_s1820.md#1aee4670435531c1425737aedfa694b6d6) () <br>Informs about presence of a **[DS1820](class_d_s1820.md)** sensor. |
|void|[**setResolution**](class_d_s1820.md#1af57f5ddaaeb4119cf6383d3f843d7a67) (uint8\_t res) <br>Sets temperature-to-digital conversion resolution. |
|void|[**startConversion**](class_d_s1820.md#1a181670cbcc211093e49a3c62f57eff5d) (void) <br>Starts temperature conversion. |
|float|[**read**](class_d_s1820.md#1a506b55951678734afa3f66e43f8e3e00) (void) <br>Reads temperature from the chip's Scratchpad. |
|uint8\_t|[**read**](class_d_s1820.md#1af46beefec88fa9b57350b5feee9a3e67) (float & temp) <br>Reads temperature from chip's scratchpad. |


## Public Functions Documentation

### function <a id="1a701b51269a6af8ccb319ea5f1eda2686" href="#1a701b51269a6af8ccb319ea5f1eda2686">DS1820</a>

```cpp
DS1820::DS1820 (
    PinName pin
)
```

Constructs a generic **[DS1820](class_d_s1820.md)** sensor. 



**Note:**

**[begin()](class_d_s1820.md#1a1fc30caa0df9ffb740cfd7e7956f4f8d)** must be called to detect and initialize the actual model 




**Parameters:**


* _pin_ Name of data pin 



**Return value:**


* __ 



### function <a id="1a3b0b002ab8834b64b0f20852a55b80af" href="#1a3b0b002ab8834b64b0f20852a55b80af">DS1820</a>

```cpp
DS1820::DS1820 (
    char model,
    PinName pin
)
```

Constructs a specific model. 



**Note:**

No need to call **[begin()](class_d_s1820.md#1a1fc30caa0df9ffb740cfd7e7956f4f8d)** to detect and initialize the model 




**Parameters:**


* _model_ One character model name: 'S', 's', 'B' or 'b' pin: Name of data pin 



**Return value:**


* __ 



### function <a id="1a1fc30caa0df9ffb740cfd7e7956f4f8d" href="#1a1fc30caa0df9ffb740cfd7e7956f4f8d">begin</a>

```cpp
bool DS1820::begin (
    void 
)
```

Detects and initializes the actual **[DS1820](class_d_s1820.md)** model. 



**Note:**






**Parameters:**


* __ 



### function <a id="1aee4670435531c1425737aedfa694b6d6" href="#1aee4670435531c1425737aedfa694b6d6">isPresent</a>

```cpp
bool DS1820::isPresent ()
```

Informs about presence of a **[DS1820](class_d_s1820.md)** sensor. 



**Note:**

**[begin()](class_d_s1820.md#1a1fc30caa0df9ffb740cfd7e7956f4f8d)** shall be called before using this function if a generic **[DS1820](class_d_s1820.md)** instance was created by the user. No need to call **[begin()](class_d_s1820.md#1a1fc30caa0df9ffb740cfd7e7956f4f8d)** for a specific **[DS1820](class_d_s1820.md)** instance. 




**Parameters:**


* __ 



### function <a id="1af57f5ddaaeb4119cf6383d3f843d7a67" href="#1af57f5ddaaeb4119cf6383d3f843d7a67">setResolution</a>

```cpp
void DS1820::setResolution (
    uint8_t res
)
```

Sets temperature-to-digital conversion resolution. 



**Note:**

The configuration register allows the user to set the resolution of the temperature-to-digital conversion to 9, 10, 11, or 12 bits. Defaults to 12-bit resolution for DS18B20. DS18S20 allows only 9-bit resolution. 




**Parameters:**


* _res_ Resolution of the temperature-to-digital conversion in bits. 



**Return value:**


* __ 



### function <a id="1a181670cbcc211093e49a3c62f57eff5d" href="#1a181670cbcc211093e49a3c62f57eff5d">startConversion</a>

```cpp
void DS1820::startConversion (
    void 
)
```

Starts temperature conversion. 



**Note:**

The time to complete the converion depends on the selected resolution: 9-bit resolution -> max conversion time = 93.75ms 10-bit resolution -> max conversion time = 187.5ms 11-bit resolution -> max conversion time = 375ms 12-bit resolution -> max conversion time = 750ms 




**Parameters:**


* __ 



### function <a id="1a506b55951678734afa3f66e43f8e3e00" href="#1a506b55951678734afa3f66e43f8e3e00">read</a>

```cpp
float DS1820::read (
    void 
)
```

Reads temperature from the chip's Scratchpad. 



**Note:**






**Parameters:**


* __ 



### function <a id="1af46beefec88fa9b57350b5feee9a3e67" href="#1af46beefec88fa9b57350b5feee9a3e67">read</a>

```cpp
uint8_t DS1820::read (
    float & temp
)
```

Reads temperature from chip's scratchpad. 



**Note:**

Verifies data integrity by calculating cyclic redundancy check (CRC). If the calculated CRC dosn't match the one stored in chip's scratchpad register the temperature variable is not updated and CRC error code is returned. 




**Parameters:**


* _temp_ The temperature variable to be updated by this routine. (It's passed as reference to floating point.) 



**Return value:**


* _error_ code: 0 - no errors ('temp' contains the temperature measured) 1 - sensor not present ('temp' is not updated) 2 - CRC error ('temp' is not updated) 





----------------------------------------
The documentation for this class was generated from the following file: `D:/w/hw-libs/\_libs\_/libraries/DS1820.h`
