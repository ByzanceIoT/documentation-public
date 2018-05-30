---
search:
    keywords: ['MPU9150', 'Ascale', 'Gscale', 'ax', 'ay', 'az', 'gx', 'gy', 'gz', 'mx', 'my', 'mz', 't', '_Ascale', '_Gscale', '_Gscalings', '_Ascalings', '_mpu', 'MPU9150', 'update_motion', 'update_mag', 'set_Ascale', 'set_Gscale', 'calibrate']
---

# class MPU9150

Driver for MPU9250 I2C accelerometer/gyroscope/magnetometer. 
## Public Types

|Type|Name|
|-----|-----|
|enum|[**Ascale**](class_m_p_u9150.md#1a71c1ff8f74e21ac25b471175106b8fd3) { **AFS\_2G** = 0, **AFS\_4G**, **AFS\_8G**, **AFS\_16G** } |
|enum|[**Gscale**](class_m_p_u9150.md#1abc72d9de20d8e905aab24b8739f7ae44) { **GFS\_250DPS** = 0, **GFS\_500DPS**, **GFS\_1000DPS**, **GFS\_2000DPS** } |


## Public Attributes

|Type|Name|
|-----|-----|
|float|[**ax**](class_m_p_u9150.md#1a5f2ddf372eb669ff1522d3eed7e70385)|
|float|[**ay**](class_m_p_u9150.md#1aa2ec1a8c11472baa67ab680ace4e569b)|
|float|[**az**](class_m_p_u9150.md#1ad20abd8127540a7f73d45006463e70e4)|
|float|[**gx**](class_m_p_u9150.md#1a01939d07391965edaedafac9c238f276)|
|float|[**gy**](class_m_p_u9150.md#1ac44f244a689fdacb6f4e36b8fc7baaa2)|
|float|[**gz**](class_m_p_u9150.md#1ad355836fc400f5f6b88bbd9215ec8de5)|
|float|[**mx**](class_m_p_u9150.md#1ad54181f3e0b8b2b5c50c1e22cae241eb)|
|float|[**my**](class_m_p_u9150.md#1a51ee749d1b0e420305e44710a429294a)|
|float|[**mz**](class_m_p_u9150.md#1ae726e537bbd5d8435031d65f60881921)|
|float|[**t**](class_m_p_u9150.md#1af56a66134cdfd53799f0d9770eabe89f)|


## Protected Attributes

|Type|Name|
|-----|-----|
|Ascale|[**\_Ascale**](class_m_p_u9150.md#1a03fdbab8ecbf838e5a1f94fc7d0ef31e)|
|Gscale|[**\_Gscale**](class_m_p_u9150.md#1a751b94761044e4318a85ca7c92dbf315)|
|const float|[**\_Gscalings**](class_m_p_u9150.md#1a21138462160722eece00f216b8ad4803)|
|const float|[**\_Ascalings**](class_m_p_u9150.md#1a989c0355258572631366174a2cb3a914)|
|**[I2CWrapper](class_i2_c_wrapper.md)**|[**\_mpu**](class_m_p_u9150.md#1a6732ce956f7e47dd97cb66b699a17fa9)|


## Public Functions

|Type|Name|
|-----|-----|
||[**MPU9150**](class_m_p_u9150.md#1a65d403f4f53952231cf8dc55714f7514) (PinName sda, PinName scl) |
|int|[**update\_motion**](class_m_p_u9150.md#1accb5819aa56df586ac8f727b1dd1c0f7) () |
|int|[**update\_mag**](class_m_p_u9150.md#1a1f84b503c4d2f6af7f967e534ddeba31) () |
|void|[**set\_Ascale**](class_m_p_u9150.md#1aed7349b18d6f4206b2dfdb59182e15bf) (Ascale scale) |
|void|[**set\_Gscale**](class_m_p_u9150.md#1ae0c1d3b6910b3781cdd8b9c85ff49915) (Gscale scale) |


## Protected Functions

|Type|Name|
|-----|-----|
|void|[**calibrate**](class_m_p_u9150.md#1ac5bf1505c8ba4939f1de70e27ff1813a) () |


## Public Types Documentation

### enum <a id="1a71c1ff8f74e21ac25b471175106b8fd3" href="#1a71c1ff8f74e21ac25b471175106b8fd3">Ascale</a>

```cpp
enum MPU9150::Ascale {
    AFS_2G = 0,
    AFS_4G,
    AFS_8G,
    AFS_16G,
};
```



### enum <a id="1abc72d9de20d8e905aab24b8739f7ae44" href="#1abc72d9de20d8e905aab24b8739f7ae44">Gscale</a>

```cpp
enum MPU9150::Gscale {
    GFS_250DPS = 0,
    GFS_500DPS,
    GFS_1000DPS,
    GFS_2000DPS,
};
```



## Public Attributes Documentation

### variable <a id="1a5f2ddf372eb669ff1522d3eed7e70385" href="#1a5f2ddf372eb669ff1522d3eed7e70385">ax</a>

```cpp
float MPU9150::ax;
```



### variable <a id="1aa2ec1a8c11472baa67ab680ace4e569b" href="#1aa2ec1a8c11472baa67ab680ace4e569b">ay</a>

```cpp
float MPU9150::ay;
```



### variable <a id="1ad20abd8127540a7f73d45006463e70e4" href="#1ad20abd8127540a7f73d45006463e70e4">az</a>

```cpp
float MPU9150::az;
```



### variable <a id="1a01939d07391965edaedafac9c238f276" href="#1a01939d07391965edaedafac9c238f276">gx</a>

```cpp
float MPU9150::gx;
```



### variable <a id="1ac44f244a689fdacb6f4e36b8fc7baaa2" href="#1ac44f244a689fdacb6f4e36b8fc7baaa2">gy</a>

```cpp
float MPU9150::gy;
```



### variable <a id="1ad355836fc400f5f6b88bbd9215ec8de5" href="#1ad355836fc400f5f6b88bbd9215ec8de5">gz</a>

```cpp
float MPU9150::gz;
```



### variable <a id="1ad54181f3e0b8b2b5c50c1e22cae241eb" href="#1ad54181f3e0b8b2b5c50c1e22cae241eb">mx</a>

```cpp
float MPU9150::mx;
```



### variable <a id="1a51ee749d1b0e420305e44710a429294a" href="#1a51ee749d1b0e420305e44710a429294a">my</a>

```cpp
float MPU9150::my;
```



### variable <a id="1ae726e537bbd5d8435031d65f60881921" href="#1ae726e537bbd5d8435031d65f60881921">mz</a>

```cpp
float MPU9150::mz;
```



### variable <a id="1af56a66134cdfd53799f0d9770eabe89f" href="#1af56a66134cdfd53799f0d9770eabe89f">t</a>

```cpp
float MPU9150::t;
```



## Protected Attributes Documentation

### variable <a id="1a03fdbab8ecbf838e5a1f94fc7d0ef31e" href="#1a03fdbab8ecbf838e5a1f94fc7d0ef31e">\_Ascale</a>

```cpp
Ascale MPU9150::_Ascale;
```



### variable <a id="1a751b94761044e4318a85ca7c92dbf315" href="#1a751b94761044e4318a85ca7c92dbf315">\_Gscale</a>

```cpp
Gscale MPU9150::_Gscale;
```



### variable <a id="1a21138462160722eece00f216b8ad4803" href="#1a21138462160722eece00f216b8ad4803">\_Gscalings</a>

```cpp
const float MPU9150::_Gscalings[4];
```



### variable <a id="1a989c0355258572631366174a2cb3a914" href="#1a989c0355258572631366174a2cb3a914">\_Ascalings</a>

```cpp
const float MPU9150::_Ascalings[4];
```



### variable <a id="1a6732ce956f7e47dd97cb66b699a17fa9" href="#1a6732ce956f7e47dd97cb66b699a17fa9">\_mpu</a>

```cpp
I2CWrapper MPU9150::_mpu;
```



## Public Functions Documentation

### function <a id="1a65d403f4f53952231cf8dc55714f7514" href="#1a65d403f4f53952231cf8dc55714f7514">MPU9150</a>

```cpp
MPU9150::MPU9150 (
    PinName sda,
    PinName scl
)
```


**[MPU9150](class_m_p_u9150.md)** constructor


**Parameters:**


* _sda_ I2C SDA pin 
* _scl_ I2C SDL pin 



### function <a id="1accb5819aa56df586ac8f727b1dd1c0f7" href="#1accb5819aa56df586ac8f727b1dd1c0f7">update\_motion</a>

```cpp
int MPU9150::update_motion ()
```


Get new data from acc/gyro sensors.


**Returns:**

0 on success, non-0 on fail 




### function <a id="1a1f84b503c4d2f6af7f967e534ddeba31" href="#1a1f84b503c4d2f6af7f967e534ddeba31">update\_mag</a>

```cpp
int MPU9150::update_mag ()
```


Get new data from magnetometer


**Returns:**

0 on success, non-0 on fail 




### function <a id="1aed7349b18d6f4206b2dfdb59182e15bf" href="#1aed7349b18d6f4206b2dfdb59182e15bf">set\_Ascale</a>

```cpp
void MPU9150::set_Ascale (
    Ascale scale
)
```



### function <a id="1ae0c1d3b6910b3781cdd8b9c85ff49915" href="#1ae0c1d3b6910b3781cdd8b9c85ff49915">set\_Gscale</a>

```cpp
void MPU9150::set_Gscale (
    Gscale scale
)
```



## Protected Functions Documentation

### function <a id="1ac5bf1505c8ba4939f1de70e27ff1813a" href="#1ac5bf1505c8ba4939f1de70e27ff1813a">calibrate</a>

```cpp
void MPU9150::calibrate ()
```





----------------------------------------
The documentation for this class was generated from the following file: `D:/w/hw-libs/\_libs\_/libraries/MPU9150.h`
