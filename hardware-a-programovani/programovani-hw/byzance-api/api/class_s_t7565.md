---
search:
    keywords: ['ST7565', 'ST7565', 'st7565_init', 'begin', 'st7565_command', 'st7565_data', 'st7565_set_brightness', 'clear_display', 'clear', 'display', 'setpixel', 'getpixel', 'fillcircle', 'drawcircle', 'drawrect', 'fillrect', 'drawline', 'drawchar', 'drawstring', 'drawstring_P', 'drawbitmap', 'drawcharPos', 'drawstringPos']
---

# class ST7565

## Public Functions

|Type|Name|
|-----|-----|
||[**ST7565**](class_s_t7565.md#1a25e995b8897b79d4f7d95bac1fc3fac9) (PinName MOSI, PinName MISO, PinName SCLK, PinName A0, PinName RST, PinName CS) |
|void|[**st7565\_init**](class_s_t7565.md#1a32e1d00377341690853c4f1b83f81f49) (void) |
|void|[**begin**](class_s_t7565.md#1a8fcb74acc724e114fcae558a305534d5) () |
|void|[**st7565\_command**](class_s_t7565.md#1a31536073a4abe6d5abbbf5eaf80ef4ac) (uint8\_t c) |
|void|[**st7565\_data**](class_s_t7565.md#1a40c70b2e9e1cba4754b66ed1190252c7) (uint8\_t c) |
|void|[**st7565\_set\_brightness**](class_s_t7565.md#1afdf532d1e35894a64dfefbf060bba41c) () |
|void|[**clear\_display**](class_s_t7565.md#1acdf4ef6c197d8c964d2003300af69a0b) (void) |
|void|[**clear**](class_s_t7565.md#1a26f02d8ced37192f785b34cd90154ee7) () |
|void|[**display**](class_s_t7565.md#1a3d1a6a9070454c84a145439484a50d70) () |
|void|[**setpixel**](class_s_t7565.md#1a5e31ef5dd1cb0fe3d0257cf37c15858e) (uint8\_t x, uint8\_t y, uint8\_t color) |
|uint8\_t|[**getpixel**](class_s_t7565.md#1a3c946caa3a1e3c8c6bddb11f71688af5) (uint8\_t x, uint8\_t y) |
|void|[**fillcircle**](class_s_t7565.md#1aba2d0e60e34c6d7faea49ddd7127358d) (uint8\_t x0, uint8\_t y0, uint8\_t r, uint8\_t color) |
|void|[**drawcircle**](class_s_t7565.md#1ad533bc6d51d1fb1bc2cb2de4c1b4b0c7) (uint8\_t x0, uint8\_t y0, uint8\_t r, uint8\_t color) |
|void|[**drawrect**](class_s_t7565.md#1ab6c7cc44268bcfea9976376d8ad5c70e) (uint8\_t x, uint8\_t y, uint8\_t w, uint8\_t h, uint8\_t color) |
|void|[**fillrect**](class_s_t7565.md#1adbdba42458bc828f289e1dc01f5a911d) (uint8\_t x, uint8\_t y, uint8\_t w, uint8\_t h, uint8\_t color) |
|void|[**drawline**](class_s_t7565.md#1a96c9b3c22be8ba1e4006abfdc624b9e0) (uint8\_t x0, uint8\_t y0, uint8\_t x1, uint8\_t y1, uint8\_t color) |
|void|[**drawchar**](class_s_t7565.md#1a96c07f70c0ef0290e216761238c09dc6) (uint8\_t x, uint8\_t line, char c) |
|void|[**drawstring**](class_s_t7565.md#1af4d46e7f297a5269317c111dfdd025c4) (uint8\_t x, uint8\_t line, char \* c) |
|void|[**drawstring\_P**](class_s_t7565.md#1a181bd213cff92d11f34101b964d22525) (uint8\_t x, uint8\_t line, const char \* c) |
|void|[**drawbitmap**](class_s_t7565.md#1ab38fb6a38d1357fef95a5a0a5d3a8632) (uint8\_t x, uint8\_t y, const uint8\_t \* bitmap, uint8\_t w, uint8\_t h, uint8\_t color) |
|void|[**drawcharPos**](class_s_t7565.md#1a997870b1a6225aa4fb2399ebef1adadb) (uint8\_t x, uint8\_t y, char c) |
|void|[**drawstringPos**](class_s_t7565.md#1af26b68fb760324b666983ed0f74f73c6) (uint8\_t x, uint8\_t y, const char \* c) |


## Public Functions Documentation

### function <a id="1a25e995b8897b79d4f7d95bac1fc3fac9" href="#1a25e995b8897b79d4f7d95bac1fc3fac9">ST7565</a>

```cpp
ST7565::ST7565 (
    PinName MOSI,
    PinName MISO,
    PinName SCLK,
    PinName A0,
    PinName RST,
    PinName CS
)
```



### function <a id="1a32e1d00377341690853c4f1b83f81f49" href="#1a32e1d00377341690853c4f1b83f81f49">st7565\_init</a>

```cpp
void ST7565::st7565_init (
    void 
)
```



### function <a id="1a8fcb74acc724e114fcae558a305534d5" href="#1a8fcb74acc724e114fcae558a305534d5">begin</a>

```cpp
void ST7565::begin ()
```



### function <a id="1a31536073a4abe6d5abbbf5eaf80ef4ac" href="#1a31536073a4abe6d5abbbf5eaf80ef4ac">st7565\_command</a>

```cpp
void ST7565::st7565_command (
    uint8_t c
)
```



### function <a id="1a40c70b2e9e1cba4754b66ed1190252c7" href="#1a40c70b2e9e1cba4754b66ed1190252c7">st7565\_data</a>

```cpp
void ST7565::st7565_data (
    uint8_t c
)
```



### function <a id="1afdf532d1e35894a64dfefbf060bba41c" href="#1afdf532d1e35894a64dfefbf060bba41c">st7565\_set\_brightness</a>

```cpp
void ST7565::st7565_set_brightness ()
```



### function <a id="1acdf4ef6c197d8c964d2003300af69a0b" href="#1acdf4ef6c197d8c964d2003300af69a0b">clear\_display</a>

```cpp
void ST7565::clear_display (
    void 
)
```



### function <a id="1a26f02d8ced37192f785b34cd90154ee7" href="#1a26f02d8ced37192f785b34cd90154ee7">clear</a>

```cpp
void ST7565::clear ()
```



### function <a id="1a3d1a6a9070454c84a145439484a50d70" href="#1a3d1a6a9070454c84a145439484a50d70">display</a>

```cpp
void ST7565::display ()
```



### function <a id="1a5e31ef5dd1cb0fe3d0257cf37c15858e" href="#1a5e31ef5dd1cb0fe3d0257cf37c15858e">setpixel</a>

```cpp
void ST7565::setpixel (
    uint8_t x,
    uint8_t y,
    uint8_t color
)
```



### function <a id="1a3c946caa3a1e3c8c6bddb11f71688af5" href="#1a3c946caa3a1e3c8c6bddb11f71688af5">getpixel</a>

```cpp
uint8_t ST7565::getpixel (
    uint8_t x,
    uint8_t y
)
```



### function <a id="1aba2d0e60e34c6d7faea49ddd7127358d" href="#1aba2d0e60e34c6d7faea49ddd7127358d">fillcircle</a>

```cpp
void ST7565::fillcircle (
    uint8_t x0,
    uint8_t y0,
    uint8_t r,
    uint8_t color
)
```



### function <a id="1ad533bc6d51d1fb1bc2cb2de4c1b4b0c7" href="#1ad533bc6d51d1fb1bc2cb2de4c1b4b0c7">drawcircle</a>

```cpp
void ST7565::drawcircle (
    uint8_t x0,
    uint8_t y0,
    uint8_t r,
    uint8_t color
)
```



### function <a id="1ab6c7cc44268bcfea9976376d8ad5c70e" href="#1ab6c7cc44268bcfea9976376d8ad5c70e">drawrect</a>

```cpp
void ST7565::drawrect (
    uint8_t x,
    uint8_t y,
    uint8_t w,
    uint8_t h,
    uint8_t color
)
```



### function <a id="1adbdba42458bc828f289e1dc01f5a911d" href="#1adbdba42458bc828f289e1dc01f5a911d">fillrect</a>

```cpp
void ST7565::fillrect (
    uint8_t x,
    uint8_t y,
    uint8_t w,
    uint8_t h,
    uint8_t color
)
```



### function <a id="1a96c9b3c22be8ba1e4006abfdc624b9e0" href="#1a96c9b3c22be8ba1e4006abfdc624b9e0">drawline</a>

```cpp
void ST7565::drawline (
    uint8_t x0,
    uint8_t y0,
    uint8_t x1,
    uint8_t y1,
    uint8_t color
)
```



### function <a id="1a96c07f70c0ef0290e216761238c09dc6" href="#1a96c07f70c0ef0290e216761238c09dc6">drawchar</a>

```cpp
void ST7565::drawchar (
    uint8_t x,
    uint8_t line,
    char c
)
```



### function <a id="1af4d46e7f297a5269317c111dfdd025c4" href="#1af4d46e7f297a5269317c111dfdd025c4">drawstring</a>

```cpp
void ST7565::drawstring (
    uint8_t x,
    uint8_t line,
    char * c
)
```



### function <a id="1a181bd213cff92d11f34101b964d22525" href="#1a181bd213cff92d11f34101b964d22525">drawstring\_P</a>

```cpp
void ST7565::drawstring_P (
    uint8_t x,
    uint8_t line,
    const char * c
)
```



### function <a id="1ab38fb6a38d1357fef95a5a0a5d3a8632" href="#1ab38fb6a38d1357fef95a5a0a5d3a8632">drawbitmap</a>

```cpp
void ST7565::drawbitmap (
    uint8_t x,
    uint8_t y,
    const uint8_t * bitmap,
    uint8_t w,
    uint8_t h,
    uint8_t color
)
```



### function <a id="1a997870b1a6225aa4fb2399ebef1adadb" href="#1a997870b1a6225aa4fb2399ebef1adadb">drawcharPos</a>

```cpp
void ST7565::drawcharPos (
    uint8_t x,
    uint8_t y,
    char c
)
```



### function <a id="1af26b68fb760324b666983ed0f74f73c6" href="#1af26b68fb760324b666983ed0f74f73c6">drawstringPos</a>

```cpp
void ST7565::drawstringPos (
    uint8_t x,
    uint8_t y,
    const char * c
)
```





----------------------------------------
The documentation for this class was generated from the following file: `D:/w/hw-libs/\_libs\_/libraries/ST7565.h`
