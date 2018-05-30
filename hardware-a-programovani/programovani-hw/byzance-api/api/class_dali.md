---
search:
    keywords: ['Dali', 'Dali', 'send', 'init']
---

# class Dali

Class to control DALI (Digital Addressable Lighting Interface) bus. 
## Public Functions

|Type|Name|
|-----|-----|
||[**Dali**](class_dali.md#1ab9aba96c89a70ab132f355990142dc42) (PinName RX, PinName TX) |
|void|[**send**](class_dali.md#1a6d656872047bebe99c06631ef959e852) (uint8\_t addr, uint8\_t cmd) |
|void|[**init**](class_dali.md#1ab3ce4681dfa3c9db82dc34dd84297ecb) () |


## Public Functions Documentation

### function <a id="1ab9aba96c89a70ab132f355990142dc42" href="#1ab9aba96c89a70ab132f355990142dc42">Dali</a>

```cpp
Dali::Dali (
    PinName RX,
    PinName TX
)
```


**[Dali](class_dali.md)** constructor


**Parameters:**


* _RX_ recieve pin 
* _TX_ transmit pin 



### function <a id="1a6d656872047bebe99c06631ef959e852" href="#1a6d656872047bebe99c06631ef959e852">send</a>

```cpp
void Dali::send (
    uint8_t addr,
    uint8_t cmd
)
```


Send command to specific short or broadcast address.


**Parameters:**


* _addr_ short/broadcast/group address 
* _command_ to send 



### function <a id="1ab3ce4681dfa3c9db82dc34dd84297ecb" href="#1ab3ce4681dfa3c9db82dc34dd84297ecb">init</a>

```cpp
void Dali::init ()
```


Init and assign short addresses. 



----------------------------------------
The documentation for this class was generated from the following file: `D:/w/hw-libs/\_libs\_/libraries/Dali.h`
