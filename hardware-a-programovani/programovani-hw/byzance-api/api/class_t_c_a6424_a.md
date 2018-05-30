---
search:
    keywords: ['TCA6424A', 'TCA6424A', 'TCA6424A', 'initialize', 'testConnection', 'readPin', 'readBank', 'readAll', 'readAll', 'getPinOutputLevel', 'getBankOutputLevel', 'getAllOutputLevel', 'getAllOutputLevel', 'writePin', 'writeBank', 'writeAll', 'writeAll', 'getPinPolarity', 'getBankPolarity', 'getAllPolarity', 'getAllPolarity', 'setPinPolarity', 'setBankPolarity', 'setAllPolarity', 'setAllPolarity', 'getPinDirection', 'getBankDirection', 'getAllDirection', 'getAllDirection', 'setPinDirection', 'setBankDirection', 'setAllDirection', 'setAllDirection']
---

# class TCA6424A

Driver for **[TCA6424A](class_t_c_a6424_a.md)** 24-bit I2C IO pin expander. 
## Public Functions

|Type|Name|
|-----|-----|
||[**TCA6424A**](class_t_c_a6424_a.md#1a8dcfc322902843c29fdfedd04a27917a) () |
||[**TCA6424A**](class_t_c_a6424_a.md#1a0d7f2559a9e000bd6127e3e7155621a4) (uint8\_t address) |
|void|[**initialize**](class_t_c_a6424_a.md#1a5bb3abff20f9dd861e881281a7494b03) (PinName sda, PinName scl) |
|bool|[**testConnection**](class_t_c_a6424_a.md#1a1bd9cad824b379b2ab4f02da2631cf58) () |
|bool|[**readPin**](class_t_c_a6424_a.md#1abb6a5d2e430105ab6d6647dc1fc2aa01) (uint16\_t pin) |
|uint8\_t|[**readBank**](class_t_c_a6424_a.md#1add9657017abb1ec3ef2f778eaa1ddae4) (uint8\_t bank) |
|bool|[**readAll**](class_t_c_a6424_a.md#1a161bd8d4c4f8c8c06e324003e5f7a03c) (uint8\_t \* banks) |
|bool|[**readAll**](class_t_c_a6424_a.md#1a24f72e5ab97dd2ae5a3c2f07c77840ed) (uint8\_t \* bank0, uint8\_t \* bank1, uint8\_t \* bank2) |
|bool|[**getPinOutputLevel**](class_t_c_a6424_a.md#1a58c2ffe40d8e32de1c7adc41a73dbb0c) (uint16\_t pin) |
|uint8\_t|[**getBankOutputLevel**](class_t_c_a6424_a.md#1a281cd0e834cfa9f2f5e7c59823577e03) (uint8\_t bank) |
|void|[**getAllOutputLevel**](class_t_c_a6424_a.md#1a07c1f0d28034b7dd0ffad694a9c217f7) (uint8\_t \* banks) |
|void|[**getAllOutputLevel**](class_t_c_a6424_a.md#1a31545217ff88f6204ce3925bdb1cb848) (uint8\_t \* bank0, uint8\_t \* bank1, uint8\_t \* bank2) |
|void|[**writePin**](class_t_c_a6424_a.md#1a1f6e7601f6f0828b76e41d08954b2389) (uint16\_t pin, bool value) |
|void|[**writeBank**](class_t_c_a6424_a.md#1af8a99d5993c1205be59f0c717da23ed8) (uint8\_t bank, uint8\_t value) |
|void|[**writeAll**](class_t_c_a6424_a.md#1aed255585660e03643d85aa0bc85031a3) (uint8\_t \* banks) |
|void|[**writeAll**](class_t_c_a6424_a.md#1afb1c204635f4bc53d5648891d9f78989) (uint8\_t bank0, uint8\_t bank1, uint8\_t bank2) |
|bool|[**getPinPolarity**](class_t_c_a6424_a.md#1ad4b497a10e4998ae0bdb3c7f9f51265b) (uint16\_t pin) |
|uint8\_t|[**getBankPolarity**](class_t_c_a6424_a.md#1a830b5cc0866e59dfc9912e71469aae39) (uint8\_t bank) |
|void|[**getAllPolarity**](class_t_c_a6424_a.md#1ab754f9857a0643081f69412dafa8d5e0) (uint8\_t \* banks) |
|void|[**getAllPolarity**](class_t_c_a6424_a.md#1a0fcb27277da2d97f2818a8b495f67a02) (uint8\_t \* bank0, uint8\_t \* bank1, uint8\_t \* bank2) |
|void|[**setPinPolarity**](class_t_c_a6424_a.md#1aa5a83bf4b1fd2a2bce2c072ee655ff41) (uint16\_t pin, bool polarity) |
|void|[**setBankPolarity**](class_t_c_a6424_a.md#1a9aab562ad4cee88b29710fceaa9c3d53) (uint8\_t bank, uint8\_t polarity) |
|void|[**setAllPolarity**](class_t_c_a6424_a.md#1ae960e337ed929333d60fff1d70780315) (uint8\_t \* banks) |
|void|[**setAllPolarity**](class_t_c_a6424_a.md#1a50004c5938a7acdc679cf7bc2328e275) (uint8\_t bank0, uint8\_t bank1, uint8\_t bank2) |
|bool|[**getPinDirection**](class_t_c_a6424_a.md#1aedd5405bd9baf732abf3bdd13c26b95a) (uint16\_t pin) |
|uint8\_t|[**getBankDirection**](class_t_c_a6424_a.md#1ac07d2c5a60d9fd60fea48783e8305c32) (uint8\_t bank) |
|void|[**getAllDirection**](class_t_c_a6424_a.md#1afdde6d24b428cff4abb3d6ca5e116389) (uint8\_t \* banks) |
|void|[**getAllDirection**](class_t_c_a6424_a.md#1a1d7f3ad0d5b18c9c2ca2ed3e78a5de39) (uint8\_t \* bank0, uint8\_t \* bank1, uint8\_t \* bank2) |
|void|[**setPinDirection**](class_t_c_a6424_a.md#1af010eb341cfc6503e32603964c22422b) (uint16\_t pin, bool direction) |
|void|[**setBankDirection**](class_t_c_a6424_a.md#1a443fd91ef564cde7d4031638ee4f89a4) (uint8\_t bank, uint8\_t direction) |
|void|[**setAllDirection**](class_t_c_a6424_a.md#1a4d8432e64db0c963ee62c65fcb745cdb) (uint8\_t \* banks) |
|void|[**setAllDirection**](class_t_c_a6424_a.md#1a15241842da4160ca06a19cbce35e12f2) (uint8\_t bank0, uint8\_t bank1, uint8\_t bank2) |


## Public Functions Documentation

### function <a id="1a8dcfc322902843c29fdfedd04a27917a" href="#1a8dcfc322902843c29fdfedd04a27917a">TCA6424A</a>

```cpp
TCA6424A::TCA6424A ()
```


Default constructor, uses default I2C address. 

**See also:**

TCA6424A\_DEFAULT\_ADDRESS 




### function <a id="1a0d7f2559a9e000bd6127e3e7155621a4" href="#1a0d7f2559a9e000bd6127e3e7155621a4">TCA6424A</a>

```cpp
TCA6424A::TCA6424A (
    uint8_t address
)
```


Specific address constructor. 

**Parameters:**


* _address_ I2C address 



**See also:**

TCA6424A\_DEFAULT\_ADDRESS 




**See also:**

TCA6424A\_ADDRESS\_ADDR\_LOW 




**See also:**

TCA6424A\_ADDRESS\_ADDR\_HIGH 




### function <a id="1a5bb3abff20f9dd861e881281a7494b03" href="#1a5bb3abff20f9dd861e881281a7494b03">initialize</a>

```cpp
void TCA6424A::initialize (
    PinName sda,
    PinName scl
)
```


Power on and prepare for general usage. The **[TCA6424A](class_t_c_a6424_a.md)** I/O expander requires no preparation after power-on. All pins will be default to INPUT mode, and the device is ready for usage immediately. This is an empty function for consistency and/or future expansion. 

### function <a id="1a1bd9cad824b379b2ab4f02da2631cf58" href="#1a1bd9cad824b379b2ab4f02da2631cf58">testConnection</a>

```cpp
bool TCA6424A::testConnection ()
```


Verify the I2C connection. Make sure the device is connected and responds as expected. 

**Returns:**

True if connection is valid, false otherwise 




### function <a id="1abb6a5d2e430105ab6d6647dc1fc2aa01" href="#1abb6a5d2e430105ab6d6647dc1fc2aa01">readPin</a>

```cpp
bool TCA6424A::readPin (
    uint16_t pin
)
```


Get a single INPUT pin's logic level. 

**Returns:**

Pin logic level (0 or 1) 




### function <a id="1add9657017abb1ec3ef2f778eaa1ddae4" href="#1add9657017abb1ec3ef2f778eaa1ddae4">readBank</a>

```cpp
uint8_t TCA6424A::readBank (
    uint8_t bank
)
```


Get all pin logic levels from one bank. 

**Parameters:**


* _bank_ Which bank to read (0/1/2 for P0\*, P1\*, P2\* respectively) 



**Returns:**

8 pins' logic levels (0 or 1 for each pin) 




### function <a id="1a161bd8d4c4f8c8c06e324003e5f7a03c" href="#1a161bd8d4c4f8c8c06e324003e5f7a03c">readAll</a>

```cpp
bool TCA6424A::readAll (
    uint8_t * banks
)
```


Get all pin logic levels from all banks. Reads into single 3-byte data container. 

**Parameters:**


* _banks_ Container for all bank's pin values (P00-P27) 



### function <a id="1a24f72e5ab97dd2ae5a3c2f07c77840ed" href="#1a24f72e5ab97dd2ae5a3c2f07c77840ed">readAll</a>

```cpp
bool TCA6424A::readAll (
    uint8_t * bank0,
    uint8_t * bank1,
    uint8_t * bank2
)
```


Get all pin logic levels from all banks. Reads into individual 1-byte containers. 

**Parameters:**


* _bank0_ Container for Bank 0's pin values (P00-P07) 
* _bank1_ Container for Bank 1's pin values (P10-P17) 
* _bank2_ Container for Bank 2's pin values (P20-P27) 



### function <a id="1a58c2ffe40d8e32de1c7adc41a73dbb0c" href="#1a58c2ffe40d8e32de1c7adc41a73dbb0c">getPinOutputLevel</a>

```cpp
bool TCA6424A::getPinOutputLevel (
    uint16_t pin
)
```


Get a single OUTPUT pin's setting. Note that this returns the level set in the flip-flop, and does not necessarily represent the actual logic level present at the pin. 

**Returns:**

Pin output setting (0 or 1) 




### function <a id="1a281cd0e834cfa9f2f5e7c59823577e03" href="#1a281cd0e834cfa9f2f5e7c59823577e03">getBankOutputLevel</a>

```cpp
uint8_t TCA6424A::getBankOutputLevel (
    uint8_t bank
)
```


Get all pin output settings from one bank. Note that this returns the level set in the flip-flop, and does not necessarily represent the actual logic level present at the pin. 

**Parameters:**


* _bank_ Which bank to read (0/1/2 for P0\*, P1\*, P2\* respectively) 



**Returns:**

8 pins' output settings (0 or 1 for each pin) 




### function <a id="1a07c1f0d28034b7dd0ffad694a9c217f7" href="#1a07c1f0d28034b7dd0ffad694a9c217f7">getAllOutputLevel</a>

```cpp
void TCA6424A::getAllOutputLevel (
    uint8_t * banks
)
```


Get all pin output settings from all banks. Reads into single 3-byte data container. 

**Parameters:**


* _banks_ Container for all bank's pin values (P00-P27) 



### function <a id="1a31545217ff88f6204ce3925bdb1cb848" href="#1a31545217ff88f6204ce3925bdb1cb848">getAllOutputLevel</a>

```cpp
void TCA6424A::getAllOutputLevel (
    uint8_t * bank0,
    uint8_t * bank1,
    uint8_t * bank2
)
```


Get all pin output settings from all banks. Reads into individual 1-byte containers. Note that this returns the level set in the flip-flop, and does not necessarily represent the actual logic level present at the pin. 

**Parameters:**


* _bank0_ Container for Bank 0's pin values (P00-P07) 
* _bank1_ Container for Bank 1's pin values (P10-P17) 
* _bank2_ Container for Bank 2's pin values (P20-P27) 



### function <a id="1a1f6e7601f6f0828b76e41d08954b2389" href="#1a1f6e7601f6f0828b76e41d08954b2389">writePin</a>

```cpp
void TCA6424A::writePin (
    uint16_t pin,
    bool value
)
```


Set a single OUTPUT pin's logic level. 

**Parameters:**


* _pin_ Which pin to write (0-23) 
* _value_ New pin output logic level (0 or 1) 



### function <a id="1af8a99d5993c1205be59f0c717da23ed8" href="#1af8a99d5993c1205be59f0c717da23ed8">writeBank</a>

```cpp
void TCA6424A::writeBank (
    uint8_t bank,
    uint8_t value
)
```


Set all OUTPUT pins' logic levels in one bank. 

**Parameters:**


* _bank_ Which bank to write (0/1/2 for P0\*, P1\*, P2\* respectively) 
* _value_ New pins' output logic level (0 or 1 for each pin) 



### function <a id="1aed255585660e03643d85aa0bc85031a3" href="#1aed255585660e03643d85aa0bc85031a3">writeAll</a>

```cpp
void TCA6424A::writeAll (
    uint8_t * banks
)
```


Set all OUTPUT pins' logic levels in all banks. 

**Parameters:**


* _banks_ All pins' new logic values (P00-P27) in 3-byte array 



### function <a id="1afb1c204635f4bc53d5648891d9f78989" href="#1afb1c204635f4bc53d5648891d9f78989">writeAll</a>

```cpp
void TCA6424A::writeAll (
    uint8_t bank0,
    uint8_t bank1,
    uint8_t bank2
)
```


Set all OUTPUT pins' logic levels in all banks. 

**Parameters:**


* _bank0_ Bank 0's new logic values (P00-P07) 
* _bank1_ Bank 1's new logic values (P10-P17) 
* _bank2_ Bank 2's new logic values (P20-P27) 



### function <a id="1ad4b497a10e4998ae0bdb3c7f9f51265b" href="#1ad4b497a10e4998ae0bdb3c7f9f51265b">getPinPolarity</a>

```cpp
bool TCA6424A::getPinPolarity (
    uint16_t pin
)
```


Get a single pin's polarity (normal/inverted) setting. 

**Returns:**

Pin polarity setting (0 or 1) 




### function <a id="1a830b5cc0866e59dfc9912e71469aae39" href="#1a830b5cc0866e59dfc9912e71469aae39">getBankPolarity</a>

```cpp
uint8_t TCA6424A::getBankPolarity (
    uint8_t bank
)
```


Get all pin polarity (normal/inverted) settings from one bank. 

**Parameters:**


* _bank_ Which bank to read (0/1/2 for P0\*, P1\*, P2\* respectively) 



**Returns:**

8 pins' polarity settings (0 or 1 for each pin) 




### function <a id="1ab754f9857a0643081f69412dafa8d5e0" href="#1ab754f9857a0643081f69412dafa8d5e0">getAllPolarity</a>

```cpp
void TCA6424A::getAllPolarity (
    uint8_t * banks
)
```


Get all pin polarity (normal/inverted) settings from all banks. Reads into single 3-byte data container. 

**Parameters:**


* _banks_ Container for all bank's pin values (P00-P27) 



### function <a id="1a0fcb27277da2d97f2818a8b495f67a02" href="#1a0fcb27277da2d97f2818a8b495f67a02">getAllPolarity</a>

```cpp
void TCA6424A::getAllPolarity (
    uint8_t * bank0,
    uint8_t * bank1,
    uint8_t * bank2
)
```


Get all pin polarity (normal/inverted) settings from all banks. Reads into individual 1-byte containers. 

**Parameters:**


* _bank0_ Container for Bank 0's pin values (P00-P07) 
* _bank1_ Container for Bank 1's pin values (P10-P17) 
* _bank2_ Container for Bank 2's pin values (P20-P27) 



### function <a id="1aa5a83bf4b1fd2a2bce2c072ee655ff41" href="#1aa5a83bf4b1fd2a2bce2c072ee655ff41">setPinPolarity</a>

```cpp
void TCA6424A::setPinPolarity (
    uint16_t pin,
    bool polarity
)
```


Set a single pin's polarity (normal/inverted) setting. 

**Parameters:**


* _pin_ Which pin to write (0-23) 
* _polarity_ New pin polarity setting (0 or 1) 



### function <a id="1a9aab562ad4cee88b29710fceaa9c3d53" href="#1a9aab562ad4cee88b29710fceaa9c3d53">setBankPolarity</a>

```cpp
void TCA6424A::setBankPolarity (
    uint8_t bank,
    uint8_t polarity
)
```


Set all pin polarity (normal/inverted) settings in one bank. 

**Parameters:**


* _bank_ Which bank to write (0/1/2 for P0\*, P1\*, P2\* respectively) 



**Returns:**

New pins' polarity settings (0 or 1 for each pin) 




### function <a id="1ae960e337ed929333d60fff1d70780315" href="#1ae960e337ed929333d60fff1d70780315">setAllPolarity</a>

```cpp
void TCA6424A::setAllPolarity (
    uint8_t * banks
)
```


Set all pin polarity (normal/inverted) settings in all banks. 

**Parameters:**


* _banks_ All pins' new logic values (P00-P27) in 3-byte array 



### function <a id="1a50004c5938a7acdc679cf7bc2328e275" href="#1a50004c5938a7acdc679cf7bc2328e275">setAllPolarity</a>

```cpp
void TCA6424A::setAllPolarity (
    uint8_t bank0,
    uint8_t bank1,
    uint8_t bank2
)
```


Set all pin polarity (normal/inverted) settings in all banks. 

**Parameters:**


* _bank0_ Bank 0's new polarity values (P00-P07) 
* _bank1_ Bank 1's new polarity values (P10-P17) 
* _bank2_ Bank 2's new polarity values (P20-P27) 



### function <a id="1aedd5405bd9baf732abf3bdd13c26b95a" href="#1aedd5405bd9baf732abf3bdd13c26b95a">getPinDirection</a>

```cpp
bool TCA6424A::getPinDirection (
    uint16_t pin
)
```


Get a single pin's direction (I/O) setting. 

**Returns:**

Pin direction setting (0 or 1) 




### function <a id="1ac07d2c5a60d9fd60fea48783e8305c32" href="#1ac07d2c5a60d9fd60fea48783e8305c32">getBankDirection</a>

```cpp
uint8_t TCA6424A::getBankDirection (
    uint8_t bank
)
```


Get all pin direction (I/O) settings from one bank. 

**Parameters:**


* _bank_ Which bank to read (0/1/2 for P0\*, P1\*, P2\* respectively) 



**Returns:**

8 pins' direction settings (0 or 1 for each pin) 




### function <a id="1afdde6d24b428cff4abb3d6ca5e116389" href="#1afdde6d24b428cff4abb3d6ca5e116389">getAllDirection</a>

```cpp
void TCA6424A::getAllDirection (
    uint8_t * banks
)
```


Get all pin direction (I/O) settings from all banks. Reads into single 3-byte data container. 

**Parameters:**


* _banks_ Container for all bank's pin values (P00-P27) 



### function <a id="1a1d7f3ad0d5b18c9c2ca2ed3e78a5de39" href="#1a1d7f3ad0d5b18c9c2ca2ed3e78a5de39">getAllDirection</a>

```cpp
void TCA6424A::getAllDirection (
    uint8_t * bank0,
    uint8_t * bank1,
    uint8_t * bank2
)
```


Get all pin direction (I/O) settings from all banks. Reads into individual 1-byte containers. 

**Parameters:**


* _bank0_ Container for Bank 0's pin values (P00-P07) 
* _bank1_ Container for Bank 1's pin values (P10-P17) 
* _bank2_ Container for Bank 2's pin values (P20-P27) 



### function <a id="1af010eb341cfc6503e32603964c22422b" href="#1af010eb341cfc6503e32603964c22422b">setPinDirection</a>

```cpp
void TCA6424A::setPinDirection (
    uint16_t pin,
    bool direction
)
```


Set a single pin's direction (I/O) setting. 

**Parameters:**


* _pin_ Which pin to write (0-23) 
* _direction_ Pin direction setting (0 or 1) 



### function <a id="1a443fd91ef564cde7d4031638ee4f89a4" href="#1a443fd91ef564cde7d4031638ee4f89a4">setBankDirection</a>

```cpp
void TCA6424A::setBankDirection (
    uint8_t bank,
    uint8_t direction
)
```


Set all pin direction (I/O) settings in one bank. 

**Parameters:**


* _bank_ Which bank to read (0/1/2 for P0\*, P1\*, P2\* respectively) 
* _direction_ New pins' direction settings (0 or 1 for each pin) 



### function <a id="1a4d8432e64db0c963ee62c65fcb745cdb" href="#1a4d8432e64db0c963ee62c65fcb745cdb">setAllDirection</a>

```cpp
void TCA6424A::setAllDirection (
    uint8_t * banks
)
```


Set all pin direction (I/O) settings in all banks. 

**Parameters:**


* _banks_ All pins' new direction values (P00-P27) in 3-byte array 



### function <a id="1a15241842da4160ca06a19cbce35e12f2" href="#1a15241842da4160ca06a19cbce35e12f2">setAllDirection</a>

```cpp
void TCA6424A::setAllDirection (
    uint8_t bank0,
    uint8_t bank1,
    uint8_t bank2
)
```


Set all pin direction (I/O) settings in all banks. 

**Parameters:**


* _bank0_ Bank 0's new direction values (P00-P07) 
* _bank1_ Bank 1's new direction values (P10-P17) 
* _bank2_ Bank 2's new direction values (P20-P27) 





----------------------------------------
The documentation for this class was generated from the following file: `D:/w/hw-libs/\_libs\_/libraries/TCA6424A.h`
