---
search:
  keywords:
    - DHT
    - eError
    - eError
    - eScale
    - DHT
    - ~DHT
    - readData
    - ReadHumidity
    - ReadTemperature
    - CalcdewPoint
    - CalcdewPointFast
---

# DHT

Class to read data from DHT11 humidity and temperature sensor.

## Public Types

| Type | Name |
| --- | --- |
| enum | [**eError**](dht.md#1a649af39fa19814c7862430a49e165d62) { **DHT11** = 11, **SEN11301P** = 11, **RHT01** = 11, **DHT22** = 22, **AM2302** = 22, **SEN51035P** = 22, **RHT02** = 22, **RHT03** = 22, **ERROR\_NONE** = 0, **BUS\_BUSY** =1, **ERROR\_NOT\_PRESENT** =2, **ERROR\_ACK\_TOO\_LONG** =3, **ERROR\_SYNC\_TIMEOUT** = 4, **ERROR\_DATA\_TIMEOUT** =5, **ERROR\_CHECKSUM** = 6, **ERROR\_NO\_PATIENCE** =7 } |
| enum | [**eError**](dht.md#1a649af39fa19814c7862430a49e165d62) { **DHT11** = 11, **SEN11301P** = 11, **RHT01** = 11, **DHT22** = 22, **AM2302** = 22, **SEN51035P** = 22, **RHT02** = 22, **RHT03** = 22, **ERROR\_NONE** = 0, **BUS\_BUSY** =1, **ERROR\_NOT\_PRESENT** =2, **ERROR\_ACK\_TOO\_LONG** =3, **ERROR\_SYNC\_TIMEOUT** = 4, **ERROR\_DATA\_TIMEOUT** =5, **ERROR\_CHECKSUM** = 6, **ERROR\_NO\_PATIENCE** =7 } |
| enum | [**eScale**](dht.md#1abad043321f886924f6833923336f634e) { **CELCIUS** =0, **FARENHEIT** =1, **KELVIN** =2 } |

## Public Functions

| Type | Name |
| --- | --- |
|  | [**DHT**](dht.md#1aaecd9f1478e898b35dc76f17c893f9d5) \(PinName pin, int DHTtype\) |
|  | [**~DHT**](dht.md#1aa3034e0207490f85b581a7700547d225) \(\) |
| int | [**readData**](dht.md#1afd1bb67764109d11492c7d10036aeddb) \(void\) |
| float | [**ReadHumidity**](dht.md#1a7ecef07fcbc57545928364cdcd47f16a) \(void\) |
| float | [**ReadTemperature**](dht.md#1af9c54e7a2a2534bceba781f9904458c0) \(eScale Scale\) |
| float | [**CalcdewPoint**](dht.md#1a710cf832d645d3df72b6c12278fcf283) \(float celsius, float humidity\) |
| float | [**CalcdewPointFast**](dht.md#1acf0bbb83753dd8bdbb0ed46dc58b9ed0) \(float celsius, float humidity\) |

## Public Types Documentation

### enum [eError](dht.md#1a649af39fa19814c7862430a49e165d62)

```cpp
enum DHT::eError {
    DHT11 = 11,
    SEN11301P = 11,
    RHT01 = 11,
    DHT22 = 22,
    AM2302 = 22,
    SEN51035P = 22,
    RHT02 = 22,
    RHT03 = 22,
    ERROR_NONE = 0,
    BUS_BUSY =1,
    ERROR_NOT_PRESENT =2,
    ERROR_ACK_TOO_LONG =3,
    ERROR_SYNC_TIMEOUT = 4,
    ERROR_DATA_TIMEOUT =5,
    ERROR_CHECKSUM = 6,
    ERROR_NO_PATIENCE =7,
};
```

### enum [eError](dht.md#1a649af39fa19814c7862430a49e165d62)

```cpp
enum DHT::eError {
    DHT11 = 11,
    SEN11301P = 11,
    RHT01 = 11,
    DHT22 = 22,
    AM2302 = 22,
    SEN51035P = 22,
    RHT02 = 22,
    RHT03 = 22,
    ERROR_NONE = 0,
    BUS_BUSY =1,
    ERROR_NOT_PRESENT =2,
    ERROR_ACK_TOO_LONG =3,
    ERROR_SYNC_TIMEOUT = 4,
    ERROR_DATA_TIMEOUT =5,
    ERROR_CHECKSUM = 6,
    ERROR_NO_PATIENCE =7,
};
```

### enum [eScale](dht.md#1abad043321f886924f6833923336f634e)

```cpp
enum DHT::eScale {
    CELCIUS =0,
    FARENHEIT =1,
    KELVIN =2,
};
```

## Public Functions Documentation

### function [DHT](dht.md#1aaecd9f1478e898b35dc76f17c893f9d5)

```cpp
DHT::DHT (
    PinName pin,
    int DHTtype
)
```

[**DHT**](dht.md) constructor

**Parameters:**

* _pin_ data pin of sensor 
* _DHTtype_ type of sensor 

### function [~DHT](dht.md#1aa3034e0207490f85b581a7700547d225)

```cpp
DHT::~DHT ()
```

### function [readData](dht.md#1afd1bb67764109d11492c7d10036aeddb)

```cpp
int DHT::readData (
    void 
)
```

read the data from sensor

**Returns:**

eError or 0 in case of no error

### function [ReadHumidity](dht.md#1a7ecef07fcbc57545928364cdcd47f16a)

```cpp
float DHT::ReadHumidity (
    void 
)
```

read last humidity, readData has to be called to update the value

**Returns:**

humidity in %

### function [ReadTemperature](dht.md#1af9c54e7a2a2534bceba781f9904458c0)

```cpp
float DHT::ReadTemperature (
    eScale Scale
)
```

read last temperature, readData has to be called to update the value

**Parameters:**

* _Scale_ select the scale \(CELCIUS, FARENHEIT or KELVIN\)

**Returns:**

temperature in selected scale

### function [CalcdewPoint](dht.md#1a710cf832d645d3df72b6c12278fcf283)

```cpp
float DHT::CalcdewPoint (
    float celsius,
    float humidity
)
```

### function [CalcdewPointFast](dht.md#1acf0bbb83753dd8bdbb0ed46dc58b9ed0)

```cpp
float DHT::CalcdewPointFast (
    float celsius,
    float humidity
)
```

The documentation for this class was generated from the following file: `D:/w/hw-libs/\_libs\_/libraries/DHT.h`

