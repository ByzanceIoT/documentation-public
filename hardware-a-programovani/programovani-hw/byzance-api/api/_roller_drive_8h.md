---
search:
    keywords: ['RollerDrive.h', 'EdgeStruct', 'RollerDrive', 'PRINTF_BINARY_PATTERN_INT8', 'PRINTF_BYTE_TO_BINARY_INT8', 'PRINTF_BINARY_PATTERN_INT16', 'PRINTF_BYTE_TO_BINARY_INT16', 'PRINTF_BINARY_PATTERN_INT32', 'PRINTF_BYTE_TO_BINARY_INT32', 'PRINTF_BINARY_PATTERN_INT64', 'PRINTF_BYTE_TO_BINARY_INT64', 'ROLLERDRIVE_TOP_RELAY_RUN', 'ROLLERDRIVE_TOP_RELAY_DIR', 'ROLLERDRIVE_BOTTOM_RELAY_RUN', 'ROLLERDRIVE_BOTTOM_RELAY_DIR', 'ROLLERDRIVE_LIGHT_AVG', 'ROLLERDRIVE_LIGHT_NONE', 'ROLLERDRIVE_LIGHT_POSTER_MARK', 'ROLLERDRIVE_LIGHT_POSTER_TOP', 'ROLLERDRIVE_LIGHT_WHITE_PAPER_MARK', 'ROLLERDRIVE_LIGHT_POSTER_NEXT', 'SYSTEM_EVENT_RUN_UP', 'SYSTEM_EVENT_STOP', 'SYSTEM_EVENT_RUN_DOWN', 'SYSTEM_EVENT_POSTER_MARK', 'SYSTEM_EVENT_WHITE_PAPER_MARK', 'SYSTEM_EVENT_POSTER_WAIT', 'SYSTEM_EVENT_IND_UP_BOTH', 'SYSTEM_EVENT_IND_UP_TOP', 'SYSTEM_EVENT_IND_UP_BOTTOM', 'SYSTEM_EVENT_IND_DOWN_BOTH', 'SYSTEM_EVENT_IND_DOWN_TOP', 'SYSTEM_EVENT_IND_DOWN_BOTTOM', 'ROLLERDRIVE_TIME_UNIT', 'ROLLERDRIVE_AUTO_MODE_PERIOD_MIN', 'ROLLERDRIVE_AUTO_MODE_PERIOD_MAX', 'ROLLERDRIVE_AUTO_MODE_PERIOD_DEFAULT', 'SIGNAL_LIGHT_SENSOR', 'MotorState', 'RollerMode']
---

# file RollerDrive.h

**[Go to the source code of this file.](_roller_drive_8h_source.md)**
## Classes

|Type|Name|
|-----|-----|
|struct|[**EdgeStruct**](struct_edge_struct.md)|
|class|[**RollerDrive**](class_roller_drive.md)|


## Defines

|Type|Name|
|-----|-----|
||[**PRINTF\_BINARY\_PATTERN\_INT8**](_roller_drive_8h.md#1a0f36e1a311176ec31284cae6677c2c33)|
||[**PRINTF\_BYTE\_TO\_BINARY\_INT8**](_roller_drive_8h.md#1a40ab2a64f481a681aac7745908cc02a6)|
||[**PRINTF\_BINARY\_PATTERN\_INT16**](_roller_drive_8h.md#1a5495cfeb1071e8f22350ac0cca7ec41e)|
||[**PRINTF\_BYTE\_TO\_BINARY\_INT16**](_roller_drive_8h.md#1ae0ac0914cef3426e841f439e594d553e)|
||[**PRINTF\_BINARY\_PATTERN\_INT32**](_roller_drive_8h.md#1a2e3529a0583fa650a07686200af65b64)|
||[**PRINTF\_BYTE\_TO\_BINARY\_INT32**](_roller_drive_8h.md#1a6df114a3f9650e1f9f8b10ad17d0ae68)|
||[**PRINTF\_BINARY\_PATTERN\_INT64**](_roller_drive_8h.md#1aeb63a617ec08ca374600de181fe6e7d0)|
||[**PRINTF\_BYTE\_TO\_BINARY\_INT64**](_roller_drive_8h.md#1ab4ad7b71eeef4677152b0bf387b23da0)|
||[**ROLLERDRIVE\_TOP\_RELAY\_RUN**](_roller_drive_8h.md#1a30063dbd30368bc1ba09aba84780f0a0)|
||[**ROLLERDRIVE\_TOP\_RELAY\_DIR**](_roller_drive_8h.md#1a3219403cd98f8e0e6625e29b35ed3eef)|
||[**ROLLERDRIVE\_BOTTOM\_RELAY\_RUN**](_roller_drive_8h.md#1a80ae7faad6d60e38ca965ae5bf5255b1)|
||[**ROLLERDRIVE\_BOTTOM\_RELAY\_DIR**](_roller_drive_8h.md#1a6047725aeefc5a27ad85785357542279)|
||[**ROLLERDRIVE\_LIGHT\_AVG**](_roller_drive_8h.md#1a4e920870e2f0b03f5b3f3e6cd5508651)|
||[**ROLLERDRIVE\_LIGHT\_NONE**](_roller_drive_8h.md#1add9c1ac876694ed3347a967f6d51daf6)|
||[**ROLLERDRIVE\_LIGHT\_POSTER\_MARK**](_roller_drive_8h.md#1a30eee77b8fc150eb50ad2c889c9ca87a)|
||[**ROLLERDRIVE\_LIGHT\_POSTER\_TOP**](_roller_drive_8h.md#1a6bf3b7c10f7927dff437104514c5996e)|
||[**ROLLERDRIVE\_LIGHT\_WHITE\_PAPER\_MARK**](_roller_drive_8h.md#1a54b5a373529aa1a8bebe35e4d3252de1)|
||[**ROLLERDRIVE\_LIGHT\_POSTER\_NEXT**](_roller_drive_8h.md#1a534d1c098617c9775bd87dee3f32be8d)|
||[**SYSTEM\_EVENT\_RUN\_UP**](_roller_drive_8h.md#1a27213e406f215f0a4481e1a42ffb1a54)|
||[**SYSTEM\_EVENT\_STOP**](_roller_drive_8h.md#1a1cd04900fd3ce1f17e28281a5794bc1b)|
||[**SYSTEM\_EVENT\_RUN\_DOWN**](_roller_drive_8h.md#1a33cc552b1a9e2355c77903a3fa2036df)|
||[**SYSTEM\_EVENT\_POSTER\_MARK**](_roller_drive_8h.md#1a48a7ff0c1aee4681d078d8e00a842b1d)|
||[**SYSTEM\_EVENT\_WHITE\_PAPER\_MARK**](_roller_drive_8h.md#1a4cbfd9439751d7a46d6dbfdb8624f7d3)|
||[**SYSTEM\_EVENT\_POSTER\_WAIT**](_roller_drive_8h.md#1a801699dc10c78c5b9a3039abe072704a)|
||[**SYSTEM\_EVENT\_IND\_UP\_BOTH**](_roller_drive_8h.md#1a7611d6cc1b9ae2c88bd52c8b4d45cd1e)|
||[**SYSTEM\_EVENT\_IND\_UP\_TOP**](_roller_drive_8h.md#1a56d2238fe39292682c4f79c458a693f5)|
||[**SYSTEM\_EVENT\_IND\_UP\_BOTTOM**](_roller_drive_8h.md#1ae7ae6348d0e3e08836458209db9da921)|
||[**SYSTEM\_EVENT\_IND\_DOWN\_BOTH**](_roller_drive_8h.md#1ae56804515c557e11c31344de60ba1044)|
||[**SYSTEM\_EVENT\_IND\_DOWN\_TOP**](_roller_drive_8h.md#1a43b599be950ec4ab5824cb802e13aa88)|
||[**SYSTEM\_EVENT\_IND\_DOWN\_BOTTOM**](_roller_drive_8h.md#1a82dfa5f157ed69a4c29504648b06b41d)|
||[**ROLLERDRIVE\_TIME\_UNIT**](_roller_drive_8h.md#1aa9215027edbf7523243d90dfd3eee8b0)|
||[**ROLLERDRIVE\_AUTO\_MODE\_PERIOD\_MIN**](_roller_drive_8h.md#1a199180983c9b110ee45751181aaaa935)|
||[**ROLLERDRIVE\_AUTO\_MODE\_PERIOD\_MAX**](_roller_drive_8h.md#1a10e19002154b2624dcbb911a7d572d4b)|
||[**ROLLERDRIVE\_AUTO\_MODE\_PERIOD\_DEFAULT**](_roller_drive_8h.md#1a1c3ef9710dca645ee0e6124008916bdb)|
||[**SIGNAL\_LIGHT\_SENSOR**](_roller_drive_8h.md#1a4fa8a91c4924df5ffa8f93fa749b1193)|


## Enums

|Type|Name|
|-----|-----|
|enum|[**MotorState**](_roller_drive_8h.md#1a518f7f0a9b3952f781fefa0bb72cddc5) { **RUN\_UP**, **STOP**, **RUN\_DOWN** } |
|enum|[**RollerMode**](_roller_drive_8h.md#1a71448c17e711aba848d633701fbed232) { **MODE\_MAN**, **MODE\_CALIB**, **MODE\_POSTER**, **MODE\_AUTO** } |


## Defines Documentation

### define <a id="1a0f36e1a311176ec31284cae6677c2c33" href="#1a0f36e1a311176ec31284cae6677c2c33">PRINTF\_BINARY\_PATTERN\_INT8</a>

```cpp
define PRINTF_BINARY_PATTERN_INT8;
```



### define <a id="1a40ab2a64f481a681aac7745908cc02a6" href="#1a40ab2a64f481a681aac7745908cc02a6">PRINTF\_BYTE\_TO\_BINARY\_INT8</a>

```cpp
define PRINTF_BYTE_TO_BINARY_INT8;
```



### define <a id="1a5495cfeb1071e8f22350ac0cca7ec41e" href="#1a5495cfeb1071e8f22350ac0cca7ec41e">PRINTF\_BINARY\_PATTERN\_INT16</a>

```cpp
define PRINTF_BINARY_PATTERN_INT16;
```



### define <a id="1ae0ac0914cef3426e841f439e594d553e" href="#1ae0ac0914cef3426e841f439e594d553e">PRINTF\_BYTE\_TO\_BINARY\_INT16</a>

```cpp
define PRINTF_BYTE_TO_BINARY_INT16;
```



### define <a id="1a2e3529a0583fa650a07686200af65b64" href="#1a2e3529a0583fa650a07686200af65b64">PRINTF\_BINARY\_PATTERN\_INT32</a>

```cpp
define PRINTF_BINARY_PATTERN_INT32;
```



### define <a id="1a6df114a3f9650e1f9f8b10ad17d0ae68" href="#1a6df114a3f9650e1f9f8b10ad17d0ae68">PRINTF\_BYTE\_TO\_BINARY\_INT32</a>

```cpp
define PRINTF_BYTE_TO_BINARY_INT32;
```



### define <a id="1aeb63a617ec08ca374600de181fe6e7d0" href="#1aeb63a617ec08ca374600de181fe6e7d0">PRINTF\_BINARY\_PATTERN\_INT64</a>

```cpp
define PRINTF_BINARY_PATTERN_INT64;
```



### define <a id="1ab4ad7b71eeef4677152b0bf387b23da0" href="#1ab4ad7b71eeef4677152b0bf387b23da0">PRINTF\_BYTE\_TO\_BINARY\_INT64</a>

```cpp
define PRINTF_BYTE_TO_BINARY_INT64;
```



### define <a id="1a30063dbd30368bc1ba09aba84780f0a0" href="#1a30063dbd30368bc1ba09aba84780f0a0">ROLLERDRIVE\_TOP\_RELAY\_RUN</a>

```cpp
define ROLLERDRIVE_TOP_RELAY_RUN;
```



### define <a id="1a3219403cd98f8e0e6625e29b35ed3eef" href="#1a3219403cd98f8e0e6625e29b35ed3eef">ROLLERDRIVE\_TOP\_RELAY\_DIR</a>

```cpp
define ROLLERDRIVE_TOP_RELAY_DIR;
```



### define <a id="1a80ae7faad6d60e38ca965ae5bf5255b1" href="#1a80ae7faad6d60e38ca965ae5bf5255b1">ROLLERDRIVE\_BOTTOM\_RELAY\_RUN</a>

```cpp
define ROLLERDRIVE_BOTTOM_RELAY_RUN;
```



### define <a id="1a6047725aeefc5a27ad85785357542279" href="#1a6047725aeefc5a27ad85785357542279">ROLLERDRIVE\_BOTTOM\_RELAY\_DIR</a>

```cpp
define ROLLERDRIVE_BOTTOM_RELAY_DIR;
```



### define <a id="1a4e920870e2f0b03f5b3f3e6cd5508651" href="#1a4e920870e2f0b03f5b3f3e6cd5508651">ROLLERDRIVE\_LIGHT\_AVG</a>

```cpp
define ROLLERDRIVE_LIGHT_AVG;
```



### define <a id="1add9c1ac876694ed3347a967f6d51daf6" href="#1add9c1ac876694ed3347a967f6d51daf6">ROLLERDRIVE\_LIGHT\_NONE</a>

```cpp
define ROLLERDRIVE_LIGHT_NONE;
```



### define <a id="1a30eee77b8fc150eb50ad2c889c9ca87a" href="#1a30eee77b8fc150eb50ad2c889c9ca87a">ROLLERDRIVE\_LIGHT\_POSTER\_MARK</a>

```cpp
define ROLLERDRIVE_LIGHT_POSTER_MARK;
```



### define <a id="1a6bf3b7c10f7927dff437104514c5996e" href="#1a6bf3b7c10f7927dff437104514c5996e">ROLLERDRIVE\_LIGHT\_POSTER\_TOP</a>

```cpp
define ROLLERDRIVE_LIGHT_POSTER_TOP;
```



### define <a id="1a54b5a373529aa1a8bebe35e4d3252de1" href="#1a54b5a373529aa1a8bebe35e4d3252de1">ROLLERDRIVE\_LIGHT\_WHITE\_PAPER\_MARK</a>

```cpp
define ROLLERDRIVE_LIGHT_WHITE_PAPER_MARK;
```



### define <a id="1a534d1c098617c9775bd87dee3f32be8d" href="#1a534d1c098617c9775bd87dee3f32be8d">ROLLERDRIVE\_LIGHT\_POSTER\_NEXT</a>

```cpp
define ROLLERDRIVE_LIGHT_POSTER_NEXT;
```



### define <a id="1a27213e406f215f0a4481e1a42ffb1a54" href="#1a27213e406f215f0a4481e1a42ffb1a54">SYSTEM\_EVENT\_RUN\_UP</a>

```cpp
define SYSTEM_EVENT_RUN_UP;
```



### define <a id="1a1cd04900fd3ce1f17e28281a5794bc1b" href="#1a1cd04900fd3ce1f17e28281a5794bc1b">SYSTEM\_EVENT\_STOP</a>

```cpp
define SYSTEM_EVENT_STOP;
```



### define <a id="1a33cc552b1a9e2355c77903a3fa2036df" href="#1a33cc552b1a9e2355c77903a3fa2036df">SYSTEM\_EVENT\_RUN\_DOWN</a>

```cpp
define SYSTEM_EVENT_RUN_DOWN;
```



### define <a id="1a48a7ff0c1aee4681d078d8e00a842b1d" href="#1a48a7ff0c1aee4681d078d8e00a842b1d">SYSTEM\_EVENT\_POSTER\_MARK</a>

```cpp
define SYSTEM_EVENT_POSTER_MARK;
```



### define <a id="1a4cbfd9439751d7a46d6dbfdb8624f7d3" href="#1a4cbfd9439751d7a46d6dbfdb8624f7d3">SYSTEM\_EVENT\_WHITE\_PAPER\_MARK</a>

```cpp
define SYSTEM_EVENT_WHITE_PAPER_MARK;
```



### define <a id="1a801699dc10c78c5b9a3039abe072704a" href="#1a801699dc10c78c5b9a3039abe072704a">SYSTEM\_EVENT\_POSTER\_WAIT</a>

```cpp
define SYSTEM_EVENT_POSTER_WAIT;
```



### define <a id="1a7611d6cc1b9ae2c88bd52c8b4d45cd1e" href="#1a7611d6cc1b9ae2c88bd52c8b4d45cd1e">SYSTEM\_EVENT\_IND\_UP\_BOTH</a>

```cpp
define SYSTEM_EVENT_IND_UP_BOTH;
```



### define <a id="1a56d2238fe39292682c4f79c458a693f5" href="#1a56d2238fe39292682c4f79c458a693f5">SYSTEM\_EVENT\_IND\_UP\_TOP</a>

```cpp
define SYSTEM_EVENT_IND_UP_TOP;
```



### define <a id="1ae7ae6348d0e3e08836458209db9da921" href="#1ae7ae6348d0e3e08836458209db9da921">SYSTEM\_EVENT\_IND\_UP\_BOTTOM</a>

```cpp
define SYSTEM_EVENT_IND_UP_BOTTOM;
```



### define <a id="1ae56804515c557e11c31344de60ba1044" href="#1ae56804515c557e11c31344de60ba1044">SYSTEM\_EVENT\_IND\_DOWN\_BOTH</a>

```cpp
define SYSTEM_EVENT_IND_DOWN_BOTH;
```



### define <a id="1a43b599be950ec4ab5824cb802e13aa88" href="#1a43b599be950ec4ab5824cb802e13aa88">SYSTEM\_EVENT\_IND\_DOWN\_TOP</a>

```cpp
define SYSTEM_EVENT_IND_DOWN_TOP;
```



### define <a id="1a82dfa5f157ed69a4c29504648b06b41d" href="#1a82dfa5f157ed69a4c29504648b06b41d">SYSTEM\_EVENT\_IND\_DOWN\_BOTTOM</a>

```cpp
define SYSTEM_EVENT_IND_DOWN_BOTTOM;
```



### define <a id="1aa9215027edbf7523243d90dfd3eee8b0" href="#1aa9215027edbf7523243d90dfd3eee8b0">ROLLERDRIVE\_TIME\_UNIT</a>

```cpp
define ROLLERDRIVE_TIME_UNIT;
```



### define <a id="1a199180983c9b110ee45751181aaaa935" href="#1a199180983c9b110ee45751181aaaa935">ROLLERDRIVE\_AUTO\_MODE\_PERIOD\_MIN</a>

```cpp
define ROLLERDRIVE_AUTO_MODE_PERIOD_MIN;
```



### define <a id="1a10e19002154b2624dcbb911a7d572d4b" href="#1a10e19002154b2624dcbb911a7d572d4b">ROLLERDRIVE\_AUTO\_MODE\_PERIOD\_MAX</a>

```cpp
define ROLLERDRIVE_AUTO_MODE_PERIOD_MAX;
```



### define <a id="1a1c3ef9710dca645ee0e6124008916bdb" href="#1a1c3ef9710dca645ee0e6124008916bdb">ROLLERDRIVE\_AUTO\_MODE\_PERIOD\_DEFAULT</a>

```cpp
define ROLLERDRIVE_AUTO_MODE_PERIOD_DEFAULT;
```



### define <a id="1a4fa8a91c4924df5ffa8f93fa749b1193" href="#1a4fa8a91c4924df5ffa8f93fa749b1193">SIGNAL\_LIGHT\_SENSOR</a>

```cpp
define SIGNAL_LIGHT_SENSOR;
```



## Enums Documentation

### enum <a id="1a518f7f0a9b3952f781fefa0bb72cddc5" href="#1a518f7f0a9b3952f781fefa0bb72cddc5">MotorState</a>

```cpp
enum RollerDrive.h::MotorState {
    RUN_UP,
    STOP,
    RUN_DOWN,
};
```



### enum <a id="1a71448c17e711aba848d633701fbed232" href="#1a71448c17e711aba848d633701fbed232">RollerMode</a>

```cpp
enum RollerDrive.h::RollerMode {
    MODE_MAN,
    MODE_CALIB,
    MODE_POSTER,
    MODE_AUTO,
};
```





----------------------------------------
The documentation for this class was generated from the following file: `D:/w/hw-libs/\_libs\_/libraries/RollerDrive.h`
