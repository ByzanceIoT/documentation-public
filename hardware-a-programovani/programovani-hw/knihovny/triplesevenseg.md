---
search:
  keywords:
    - TripleSevenSeg
    - TripleSevenSeg
    - is_initialized
    - display_number
    - display_symbol
---

# TripleSevenSeg

Driver to control three-digits 7-segment LED display on LED shield.

## Public Functions

| Type | Name |
| --- | --- |
|  | [**TripleSevenSeg**](triplesevenseg.md#1a58cb5aac681147422f9d0b60bc59468a) \(\) |
| bool | [**is\_initialized**](triplesevenseg.md#1a70c5a71e0de4e3113579349d80c8eea4) \(void\) |
| bool | [**display\_number**](triplesevenseg.md#1a8a642c977098e19839df2bade70a45ea) \(float value, uint8\_t decimal\_positions\) |
| uint32\_t | [**display\_symbol**](triplesevenseg.md#1a7b514d75df52bc75c45f18edf9ab5c59) \(char symbol, uint8\_t position, bool dot\) |

## Public Functions Documentation

### function [TripleSevenSeg](triplesevenseg.md#1a58cb5aac681147422f9d0b60bc59468a)

```cpp
TripleSevenSeg::TripleSevenSeg ()
```

### function [is\_initialized](triplesevenseg.md#1a70c5a71e0de4e3113579349d80c8eea4)

```cpp
bool TripleSevenSeg::is_initialized (
    void 
)
```

Is driver initialized?

### function [display\_number](triplesevenseg.md#1a8a642c977098e19839df2bade70a45ea)

```cpp
bool TripleSevenSeg::display_number (
    float value,
    uint8_t decimal_positions
)
```

Display float value on seven segment display. Supports positive and negative numbers in range from -99 to 999.

**Parameters:**

* _value_ Value to display. 
* _decimal\_positions_ Maximal number of displayed decimal positions. 

### function [display\_symbol](triplesevenseg.md#1a7b514d75df52bc75c45f18edf9ab5c59)

```cpp
uint32_t TripleSevenSeg::display_symbol (
    char symbol,
    uint8_t position,
    bool dot
)
```

Display supported symbol to LED segment at specified position with optional decimal point.

**Parameters:**

* _symbol_ Supported symbol. 
* _position_ Position on LED display. 
* _show_ decimal point 

The documentation for this class was generated from the following file: `D:/w/hw-libs/\_libs\_/libraries/TripleSevenSeg.h`

