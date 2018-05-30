---
search:
    keywords: ['OneWire', 'OneWire', 'reset', 'select', 'skip', 'write', 'write_bytes', 'read', 'read_bytes', 'write_bit', 'read_bit', 'depower', 'reset_search', 'target_search', 'search', 'crc8']
---

# class OneWire

## Public Functions

|Type|Name|
|-----|-----|
||[**OneWire**](class_one_wire.md#1a9363813c295003567ee1f2b24a2b3dc9) (PinName pin) |
|uint8\_t|[**reset**](class_one_wire.md#1a6a742a9112392567eae3d06dde067c07) (void) |
|void|[**select**](class_one_wire.md#1accf808390abd63d3c7bce35677784384) (const uint8\_t rom) |
|void|[**skip**](class_one_wire.md#1ae3780e2b0ea2ebf6be88298412ac7798) (void) |
|void|[**write**](class_one_wire.md#1a843e9e7e57ed615b4880be0b76b40b7d) (uint8\_t v, uint8\_t power = 0) |
|void|[**write\_bytes**](class_one_wire.md#1a0fc1e0bdc2ab1f062c98567fa60a69ae) (const uint8\_t \* buf, uint16\_t count, bool power = 0) |
|uint8\_t|[**read**](class_one_wire.md#1afd9bdb8b5a5b69b394dfc76352e00e21) (void) |
|void|[**read\_bytes**](class_one_wire.md#1a2407440e8e25b624617593f8ad6447d4) (uint8\_t \* buf, uint16\_t count) |
|void|[**write\_bit**](class_one_wire.md#1a6bbc58276d1cb08653dab3ea35378f94) (uint8\_t v) |
|uint8\_t|[**read\_bit**](class_one_wire.md#1aeae4c2798b70d9d0ba3091c03ee2d056) (void) |
|void|[**depower**](class_one_wire.md#1aa8e0f62e830ad05d8035e55c7a309256) (void) |
|void|[**reset\_search**](class_one_wire.md#1aae5efdf67928b5ee312ab7d7906416fa) () |
|void|[**target\_search**](class_one_wire.md#1a0a1b8457adb609a693b865dd474e5116) (uint8\_t family\_code) |
|uint8\_t|[**search**](class_one_wire.md#1a383dc74fc9f8a27b76366a2859c3820a) (uint8\_t \* newAddr) |


## Public Static Functions

|Type|Name|
|-----|-----|
|static uint8\_t|[**crc8**](class_one_wire.md#1ae3486a669581b750e4fdf3f3a12b05f1) (const uint8\_t \* addr, uint8\_t len) |


## Public Functions Documentation

### function <a id="1a9363813c295003567ee1f2b24a2b3dc9" href="#1a9363813c295003567ee1f2b24a2b3dc9">OneWire</a>

```cpp
OneWire::OneWire (
    PinName pin
)
```



### function <a id="1a6a742a9112392567eae3d06dde067c07" href="#1a6a742a9112392567eae3d06dde067c07">reset</a>

```cpp
uint8_t OneWire::reset (
    void 
)
```



### function <a id="1accf808390abd63d3c7bce35677784384" href="#1accf808390abd63d3c7bce35677784384">select</a>

```cpp
void OneWire::select (
    const uint8_t rom
)
```



### function <a id="1ae3780e2b0ea2ebf6be88298412ac7798" href="#1ae3780e2b0ea2ebf6be88298412ac7798">skip</a>

```cpp
void OneWire::skip (
    void 
)
```



### function <a id="1a843e9e7e57ed615b4880be0b76b40b7d" href="#1a843e9e7e57ed615b4880be0b76b40b7d">write</a>

```cpp
void OneWire::write (
    uint8_t v,
    uint8_t power = 0
)
```



### function <a id="1a0fc1e0bdc2ab1f062c98567fa60a69ae" href="#1a0fc1e0bdc2ab1f062c98567fa60a69ae">write\_bytes</a>

```cpp
void OneWire::write_bytes (
    const uint8_t * buf,
    uint16_t count,
    bool power = 0
)
```



### function <a id="1afd9bdb8b5a5b69b394dfc76352e00e21" href="#1afd9bdb8b5a5b69b394dfc76352e00e21">read</a>

```cpp
uint8_t OneWire::read (
    void 
)
```



### function <a id="1a2407440e8e25b624617593f8ad6447d4" href="#1a2407440e8e25b624617593f8ad6447d4">read\_bytes</a>

```cpp
void OneWire::read_bytes (
    uint8_t * buf,
    uint16_t count
)
```



### function <a id="1a6bbc58276d1cb08653dab3ea35378f94" href="#1a6bbc58276d1cb08653dab3ea35378f94">write\_bit</a>

```cpp
void OneWire::write_bit (
    uint8_t v
)
```



### function <a id="1aeae4c2798b70d9d0ba3091c03ee2d056" href="#1aeae4c2798b70d9d0ba3091c03ee2d056">read\_bit</a>

```cpp
uint8_t OneWire::read_bit (
    void 
)
```



### function <a id="1aa8e0f62e830ad05d8035e55c7a309256" href="#1aa8e0f62e830ad05d8035e55c7a309256">depower</a>

```cpp
void OneWire::depower (
    void 
)
```



### function <a id="1aae5efdf67928b5ee312ab7d7906416fa" href="#1aae5efdf67928b5ee312ab7d7906416fa">reset\_search</a>

```cpp
void OneWire::reset_search ()
```



### function <a id="1a0a1b8457adb609a693b865dd474e5116" href="#1a0a1b8457adb609a693b865dd474e5116">target\_search</a>

```cpp
void OneWire::target_search (
    uint8_t family_code
)
```



### function <a id="1a383dc74fc9f8a27b76366a2859c3820a" href="#1a383dc74fc9f8a27b76366a2859c3820a">search</a>

```cpp
uint8_t OneWire::search (
    uint8_t * newAddr
)
```



## Public Static Functions Documentation

### function <a id="1ae3486a669581b750e4fdf3f3a12b05f1" href="#1ae3486a669581b750e4fdf3f3a12b05f1">crc8</a>

```cpp
static uint8_t OneWire::crc8 (
    const uint8_t * addr,
    uint8_t len
)
```





----------------------------------------
The documentation for this class was generated from the following file: `D:/w/hw-libs/\_libs\_/libraries/OneWire.h`
