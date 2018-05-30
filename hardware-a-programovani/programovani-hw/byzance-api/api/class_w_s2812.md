---
search:
    keywords: ['WS2812', 'WS2812', '~WS2812', 'write', 'write_offsets', 'setAll', 'useII', 'setII']
---

# class WS2812

Library for the **[WS2812](class_w_s2812.md)** RGB LED with integrated controller. [More...](#detailed-description)
## Public Functions

|Type|Name|
|-----|-----|
||[**WS2812**](class_w_s2812.md#1a66f401813e323c32f2a2faee95ad0ac8) (PinName d, int size) <br>Creates an instance of the class. |
||[**~WS2812**](class_w_s2812.md#1a58973dedd9cbc5c3fd3397f07f9a720f) () |
|void|[**write**](class_w_s2812.md#1ab85d6a78bc51929dac48db05f6bc68d4) (int buf) |
|void|[**write\_offsets**](class_w_s2812.md#1a578fd0b278445bd6f84e260a69b18a68) (int buf, int r\_offset = 0, int g\_offset = 0, int b\_offset = 0) |
|void|[**setAll**](class_w_s2812.md#1a49eb3ad0ca20b705915315b295e20702) (int colour) |
|void|[**useII**](class_w_s2812.md#1a0538d36939ccfe9cf0e2fb5a2568ca93) (int d) |
|void|[**setII**](class_w_s2812.md#1a8b6491617f9beb271d6d5c56ba384fb6) (unsigned char II) |


## Detailed Description

The **[WS2812](class_w_s2812.md)** is controller that is built into a range of LEDs 
## Public Functions Documentation

### function <a id="1a66f401813e323c32f2a2faee95ad0ac8" href="#1a66f401813e323c32f2a2faee95ad0ac8">WS2812</a>

```cpp
WS2812::WS2812 (
    PinName d,
    int size
)
```

Creates an instance of the class. 

Connect **[WS2812](class_w_s2812.md)** address addr using SPI MOSI pins **[WS2812](class_w_s2812.md)** constructor.


**Parameters:**


* _d_ SPI MOSI pin (data pin of **[WS2812](class_w_s2812.md)**) 
* _size_ number of RGB LEDs on stripe 



### function <a id="1a58973dedd9cbc5c3fd3397f07f9a720f" href="#1a58973dedd9cbc5c3fd3397f07f9a720f">~WS2812</a>

```cpp
WS2812::~WS2812 ()
```



### function <a id="1ab85d6a78bc51929dac48db05f6bc68d4" href="#1ab85d6a78bc51929dac48db05f6bc68d4">write</a>

```cpp
void WS2812::write (
    int buf
)
```


Writes data to bus asynchronously.


**Parameters:**


* _buf_ pointer to buffer to write 



### function <a id="1a578fd0b278445bd6f84e260a69b18a68" href="#1a578fd0b278445bd6f84e260a69b18a68">write\_offsets</a>

```cpp
void WS2812::write_offsets (
    int buf,
    int r_offset = 0,
    int g_offset = 0,
    int b_offset = 0
)
```



### function <a id="1a49eb3ad0ca20b705915315b295e20702" href="#1a49eb3ad0ca20b705915315b295e20702">setAll</a>

```cpp
void WS2812::setAll (
    int colour
)
```


Set all LEDs to the same color


**Parameters:**


* _colour_ color to set 



### function <a id="1a0538d36939ccfe9cf0e2fb5a2568ca93" href="#1a0538d36939ccfe9cf0e2fb5a2568ca93">useII</a>

```cpp
void WS2812::useII (
    int d
)
```



### function <a id="1a8b6491617f9beb271d6d5c56ba384fb6" href="#1a8b6491617f9beb271d6d5c56ba384fb6">setII</a>

```cpp
void WS2812::setII (
    unsigned char II
)
```





----------------------------------------
The documentation for this class was generated from the following file: `D:/w/hw-libs/\_libs\_/libraries/WS2812.h`
