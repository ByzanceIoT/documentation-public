---
search:
    keywords: ['SHT21', 'SHT21', 'readTemp', 'readHumidity', 'reset', 'setPrecision']
---

# class SHT21

Driver for **[SHT21](class_s_h_t21.md)** I2C temperature and humidity sensor. [More...](#detailed-description)
## Public Functions

|Type|Name|
|-----|-----|
||[**SHT21**](class_s_h_t21.md#1add548804bebe3aa63d65920a452392eb) (I2C \* i2c) |
|float|[**readTemp**](class_s_h_t21.md#1a4b9977332ee233134ceff6e3c8a95e66) () |
|float|[**readHumidity**](class_s_h_t21.md#1a8bf9612797cd5e91dbfc58c00c5331d8) () |
|int|[**reset**](class_s_h_t21.md#1a7bf9780363bfa7716998ce2c69469eab) () |
|int|[**setPrecision**](class_s_h_t21.md#1acab92c5370b303580dcf5236f1a8991e) (char precision) |


## Detailed Description

**[SHT21](class_s_h_t21.md)** Connection class, utilizing a I2C interface
Example: 
```cpp
#include "mbed.h"
#include "SHT21_ncleee.h"


DigitalOut myled(LED1);
Serial pc(USBTX, USBRX);
I2C i2c(p28,p27);
SHT21 sht(&i2c);

int main() 
{

    pc.printf("Hello World...\n\tTesting temperature Sensor\n");
    
    int temperature = sht.readTemp();

    pc.printf("Temperature is: %d \n", temperature);
    
    pc.printf("Experiment complete...\n");

}
```

 
## Public Functions Documentation

### function <a id="1add548804bebe3aa63d65920a452392eb" href="#1add548804bebe3aa63d65920a452392eb">SHT21</a>

```cpp
SHT21::SHT21 (
    I2C * i2c
)
```


Constructor - create a connection to a **[SHT21](class_s_h_t21.md)** temperature and humidity sensor through an I2C interface


**Parameters:**


* _\*i2c_ a pointer to the i2c interface that is used for communication 
* _frequency_ - I2C frequency 



### function <a id="1a4b9977332ee233134ceff6e3c8a95e66" href="#1a4b9977332ee233134ceff6e3c8a95e66">readTemp</a>

```cpp
float SHT21::readTemp ()
```


Read the temperature value from the sensor 
 Involves triggering the measuring unit then waiting for 100ms for the measuring to complete before reading the temperature 
 

**Parameters:**


* _returns_ a value representing the temperature in degrees centigrade 



### function <a id="1a8bf9612797cd5e91dbfc58c00c5331d8" href="#1a8bf9612797cd5e91dbfc58c00c5331d8">readHumidity</a>

```cpp
float SHT21::readHumidity ()
```


Read the humidity value from the sensor 
 Involves triggering the measuring unit then waiting for 100ms for the measuring to complete before reading the humidity 
 

**Parameters:**


* _returns_ the percentage humidity 



### function <a id="1a7bf9780363bfa7716998ce2c69469eab" href="#1a7bf9780363bfa7716998ce2c69469eab">reset</a>

```cpp
int SHT21::reset ()
```


Perform a soft-reset of the sensor unit. 

### function <a id="1acab92c5370b303580dcf5236f1a8991e" href="#1acab92c5370b303580dcf5236f1a8991e">setPrecision</a>

```cpp
int SHT21::setPrecision (
    char precision
)
```


Set the precision of the measuring
//Data precision settings 
 //RH 12 T 14 - default 
 #define SHT\_PREC\_1214 0x00 
 //RH 8 T 10 
 #define SHT\_PREC\_0812 0x01 
 //RH 10 T 13 
 #define SHT\_PREC\_1013 0x80 
 //RH 11 T 11 
 #define SHT\_PREC\_1111 0x81 
 

**Parameters:**


* _precision_ - the precision, refer to above or datasheet. 





----------------------------------------
The documentation for this class was generated from the following file: `D:/w/hw-libs/\_libs\_/libraries/SHT21\_ncleee.h`
