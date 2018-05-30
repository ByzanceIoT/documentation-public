---
search:
    keywords: ['ms5637', '_i2c', 'ms5637', 'cmd_reset', 'calcTemp', 'calcPressure', 'getPressure', 'getAltitudeFT', 'getSeaLevelBaroFT', 'getSeaLevelBaroM']
---

# class ms5637

## Protected Attributes

|Type|Name|
|-----|-----|
|I2C \*|[**\_i2c**](classms5637.md#1a16075e99af9ecc315a3c201a3ce2f14c)|


## Public Functions

|Type|Name|
|-----|-----|
||[**ms5637**](classms5637.md#1a8eea062ed7ea80f1004435a22d1ede2b) (I2C \* i2c) |
|int8\_t|[**cmd\_reset**](classms5637.md#1a9ee48bae703e9b113d62b642b74d438c) () <br>send reset sequence |
|double|[**calcTemp**](classms5637.md#1a7e404b21d43c078999e368375332e895) () <br>calculate temperature |
|double|[**calcPressure**](classms5637.md#1a9c8006b9b6b67799121ce886e8f9d908) () <br>calculate pressure |
|double|[**getPressure**](classms5637.md#1ac851db4b6bc9982abd50f76625c7dd44) () <br>get pressure, no calculation |
|float|[**getAltitudeFT**](classms5637.md#1ad81e5c9b4c692d0719668d1a9a6a2bd7) (float sea\_pressure) <br>get altitude from known sea level barometer, @ no pre-pressure calculation |
|float|[**getSeaLevelBaroFT**](classms5637.md#1a50ae30f73590c7fb299b41ab617aa53f) (float known\_alt) <br>get sea level pressure from known altitude(ft), @ no pre-pressure calculation |
|float|[**getSeaLevelBaroM**](classms5637.md#1a33410471b4f3fa53cfcfa449812e1c71) (float known\_alt) <br>get sea level pressure from known altitude(m), @ no pre-pressure calculation |


## Detailed Description

Create **[ms5637](classms5637.md)** controller class


**Parameters:**


* _**[ms5637](classms5637.md)**_ class 


## Protected Attributes Documentation

### variable <a id="1a16075e99af9ecc315a3c201a3ce2f14c" href="#1a16075e99af9ecc315a3c201a3ce2f14c">\_i2c</a>

```cpp
I2C* ms5637::_i2c;
```



## Public Functions Documentation

### function <a id="1a8eea062ed7ea80f1004435a22d1ede2b" href="#1a8eea062ed7ea80f1004435a22d1ede2b">ms5637</a>

```cpp
ms5637::ms5637 (
    I2C * i2c
)
```


Create a MS5637 object using the specified I2C object


**Parameters:**


* _constructor_ the I2C object to communicate with 



### function <a id="1a9ee48bae703e9b113d62b642b74d438c" href="#1a9ee48bae703e9b113d62b642b74d438c">cmd\_reset</a>

```cpp
int8_t ms5637::cmd_reset ()
```

send reset sequence 

Initialize the MS5637 and set up the coefficients First - reset the MS5637 Second - load coefficient values from the MS5637 PROM Third - calculate coefficient checksum This routine only needs to be run once at boot up


**Parameters:**


* _NONE_ 



**Returns:**

-1 on fail, 0 on success 




### function <a id="1a7e404b21d43c078999e368375332e895" href="#1a7e404b21d43c078999e368375332e895">calcTemp</a>

```cpp
double ms5637::calcTemp ()
```

calculate temperature 

Calculate and return compensated temperature Returns double temperature in degC


**Parameters:**


* _NONE_ 



**Returns:**

double temperature degC 




### function <a id="1a9c8006b9b6b67799121ce886e8f9d908" href="#1a9c8006b9b6b67799121ce886e8f9d908">calcPressure</a>

```cpp
double ms5637::calcPressure ()
```

calculate pressure 

Calculate and return compensated barometric pressure Returns double pressure in millibars


**Parameters:**


* _NONE_ 



**Returns:**

double barometric pressure millibar 




### function <a id="1ac851db4b6bc9982abd50f76625c7dd44" href="#1ac851db4b6bc9982abd50f76625c7dd44">getPressure</a>

```cpp
double ms5637::getPressure ()
```

get pressure, no calculation 

Return compensated barometric pressure Returns double pressure in millibars DOES NOT RE-CALCULATE FIRST!!! Saves time if you **[calcTemp()](classms5637.md#1a7e404b21d43c078999e368375332e895)**; first


**Parameters:**


* _NONE_ 



**Returns:**

double barometric pressure millibar 




### function <a id="1ad81e5c9b4c692d0719668d1a9a6a2bd7" href="#1ad81e5c9b4c692d0719668d1a9a6a2bd7">getAltitudeFT</a>

```cpp
float ms5637::getAltitudeFT (
    float sea_pressure
)
```

get altitude from known sea level barometer, @ no pre-pressure calculation 

Calculate and returns altitude in feet Returns float altitude in feet


**Parameters:**


* _float_ known pressure (mB) at sea level

float sea level barometer 

**Returns:**

float altitude in feet 




### function <a id="1a50ae30f73590c7fb299b41ab617aa53f" href="#1a50ae30f73590c7fb299b41ab617aa53f">getSeaLevelBaroFT</a>

```cpp
float ms5637::getSeaLevelBaroFT (
    float known_alt
)
```

get sea level pressure from known altitude(ft), @ no pre-pressure calculation 

Calculate and returns sea level baro Returns float seal level barometer in feet


**Parameters:**


* _float_ known altitude in feet

float known altitude in feet 

**Returns:**

float seal level barometer in mb 




### function <a id="1a33410471b4f3fa53cfcfa449812e1c71" href="#1a33410471b4f3fa53cfcfa449812e1c71">getSeaLevelBaroM</a>

```cpp
float ms5637::getSeaLevelBaroM (
    float known_alt
)
```

get sea level pressure from known altitude(m), @ no pre-pressure calculation 

Calculate and returns sea level baro Returns float seal level barometer in meters


**Parameters:**


* _float_ known altitude in meters

float known altitude in meters 

**Returns:**

float seal level barometer in mb 






----------------------------------------
The documentation for this class was generated from the following file: `D:/w/hw-libs/\_libs\_/libraries/ms5637.h`
