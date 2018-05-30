---
search:
    keywords: ['Knock.h', 'Knock', 'NUMBER_OF_SAMPLES', 'ACC_THRESHOLD', 'MIC_THRESHOLD', 'TIME_WAITING', 'TIME_PEAK', 'TIME_AFTER', 'knock_stage_t', 'sensor_event_t']
---

# file Knock.h

**[Go to the source code of this file.](_knock_8h_source.md)**
## Classes

|Type|Name|
|-----|-----|
|class|[**Knock**](class_knock.md)|


## Defines

|Type|Name|
|-----|-----|
||[**NUMBER\_OF\_SAMPLES**](_knock_8h.md#1a3992a43fac1d452edf605ff497a25030)|
||[**ACC\_THRESHOLD**](_knock_8h.md#1ae40e86a65d75f2d7e076f6b24602d128)|
||[**MIC\_THRESHOLD**](_knock_8h.md#1a64f7debbe0fc9e7c16625cf7a0e5ed6f)|
||[**TIME\_WAITING**](_knock_8h.md#1a3388d73478f02b062cf0a61ca88a0bbb)|
||[**TIME\_PEAK**](_knock_8h.md#1a19b33911acf1dade14c24c7e7a653cea)|
||[**TIME\_AFTER**](_knock_8h.md#1a916ce867809fd6265b490486b6891210)|


## Enums

|Type|Name|
|-----|-----|
|enum|[**knock\_stage\_t**](_knock_8h.md#1af77f05c6a46d85750015085a2a608de7) { **KNOCK\_STAGE\_WAITING**, **KNOCK\_STAGE\_PEAK**, **KNOCK\_STAGE\_AFTER** } |
|enum|[**sensor\_event\_t**](_knock_8h.md#1ac7510a6e009db09fb95119a3ea3c94dc) { **SENSOR\_EVENT\_NONE**, **SENSOR\_EVENT\_RISE**, **SENSOR\_EVENT\_FALL** } |


## Defines Documentation

### define <a id="1a3992a43fac1d452edf605ff497a25030" href="#1a3992a43fac1d452edf605ff497a25030">NUMBER\_OF\_SAMPLES</a>

```cpp
define NUMBER_OF_SAMPLES;
```



### define <a id="1ae40e86a65d75f2d7e076f6b24602d128" href="#1ae40e86a65d75f2d7e076f6b24602d128">ACC\_THRESHOLD</a>

```cpp
define ACC_THRESHOLD;
```



### define <a id="1a64f7debbe0fc9e7c16625cf7a0e5ed6f" href="#1a64f7debbe0fc9e7c16625cf7a0e5ed6f">MIC\_THRESHOLD</a>

```cpp
define MIC_THRESHOLD;
```



### define <a id="1a3388d73478f02b062cf0a61ca88a0bbb" href="#1a3388d73478f02b062cf0a61ca88a0bbb">TIME\_WAITING</a>

```cpp
define TIME_WAITING;
```



### define <a id="1a19b33911acf1dade14c24c7e7a653cea" href="#1a19b33911acf1dade14c24c7e7a653cea">TIME\_PEAK</a>

```cpp
define TIME_PEAK;
```



### define <a id="1a916ce867809fd6265b490486b6891210" href="#1a916ce867809fd6265b490486b6891210">TIME\_AFTER</a>

```cpp
define TIME_AFTER;
```



## Enums Documentation

### enum <a id="1af77f05c6a46d85750015085a2a608de7" href="#1af77f05c6a46d85750015085a2a608de7">knock\_stage\_t</a>

```cpp
enum Knock.h::knock_stage_t {
    KNOCK_STAGE_WAITING,
    KNOCK_STAGE_PEAK,
    KNOCK_STAGE_AFTER,
};
```



### enum <a id="1ac7510a6e009db09fb95119a3ea3c94dc" href="#1ac7510a6e009db09fb95119a3ea3c94dc">sensor\_event\_t</a>

```cpp
enum Knock.h::sensor_event_t {
    SENSOR_EVENT_NONE,
    SENSOR_EVENT_RISE,
    SENSOR_EVENT_FALL,
};
```





----------------------------------------
The documentation for this class was generated from the following file: `D:/w/hw-libs/\_libs\_/libraries/Knock.h`
