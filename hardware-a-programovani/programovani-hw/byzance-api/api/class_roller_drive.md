---
search:
    keywords: ['RollerDrive', 'RollerDrive', 'set_poster', 'set_mode', 'set_auto_mode_period', 'set_auto_mode_range', 'calibration', 'is_calibrated', 'get_poster_count', 'run_ind_motors_up', 'run_ind_motors_down', 'run_ind_motors_stop', 'test_get_state_now', 'test_get_state_last', 'test_set_event', 'test_rele', 'test_io']
---

# class RollerDrive

## Public Functions

|Type|Name|
|-----|-----|
||[**RollerDrive**](class_roller_drive.md#1a576ae4f2892d32129f206fa4391722e6) (void) |
|uint8\_t|[**set\_poster**](class_roller_drive.md#1a826e3597785562f5f4aaee7f92d50469) (uint8\_t dst) |
|uint8\_t|[**set\_mode**](class_roller_drive.md#1a31aedc32f379a62933dd8e951413a6e7) (RollerMode mode) |
|uint8\_t|[**set\_auto\_mode\_period**](class_roller_drive.md#1a807ac282c15142933d3a77ccb4bef2f8) (uint32\_t period\_ms) |
|uint8\_t|[**set\_auto\_mode\_range**](class_roller_drive.md#1a6f6648a530348374af71d03727241937) (uint8\_t from, uint8\_t to) |
|uint8\_t|[**calibration**](class_roller_drive.md#1a3813a295ef72fa6e6178871106865c12) (void) |
|bool|[**is\_calibrated**](class_roller_drive.md#1ad38a994acf76e19cf7e82cb271a263f6) (void) |
|uint8\_t|[**get\_poster\_count**](class_roller_drive.md#1a7eb6ce4ec43e09ca43cd3a9c5aba063f) (void) |
|uint8\_t|[**run\_ind\_motors\_up**](class_roller_drive.md#1af02f027daafbc3b6f667b979648b5cf0) (bool top = false, bool bottom = false) |
|uint8\_t|[**run\_ind\_motors\_down**](class_roller_drive.md#1a241b6e3c6e2f5c45fe44621aec32ce5e) (bool top = false, bool bottom = false) |
|uint8\_t|[**run\_ind\_motors\_stop**](class_roller_drive.md#1a024f0ec86ffc0790be499f3431415245) () |
|uint32\_t|[**test\_get\_state\_now**](class_roller_drive.md#1abdf8cf265ca01a0975f5cf4a2e05c121) (void) |
|uint32\_t|[**test\_get\_state\_last**](class_roller_drive.md#1adbe96fee8c0882084ddd2ed6f0c0daec) (void) |
|void|[**test\_set\_event**](class_roller_drive.md#1abd808c999d69d9d1d3ef76dfd2bfdc4e) (uint32\_t event) |
|void|[**test\_rele**](class_roller_drive.md#1a416e676d5b72714ff5ce87a31f19f653) (uint8\_t val) |
|void|[**test\_io**](class_roller_drive.md#1aaf762b739d1de55cc4c0db786dcbff69) (void) |


## Public Functions Documentation

### function <a id="1a576ae4f2892d32129f206fa4391722e6" href="#1a576ae4f2892d32129f206fa4391722e6">RollerDrive</a>

```cpp
RollerDrive::RollerDrive (
    void 
)
```



### function <a id="1a826e3597785562f5f4aaee7f92d50469" href="#1a826e3597785562f5f4aaee7f92d50469">set\_poster</a>

```cpp
uint8_t RollerDrive::set_poster (
    uint8_t dst
)
```


Set poster you want do display. Range is 1 to N (N = posters count). 

### function <a id="1a31aedc32f379a62933dd8e951413a6e7" href="#1a31aedc32f379a62933dd8e951413a6e7">set\_mode</a>

```cpp
uint8_t RollerDrive::set_mode (
    RollerMode mode
)
```


Select mode of operation. Some mode requires successfully finished calibration. 

### function <a id="1a807ac282c15142933d3a77ccb4bef2f8" href="#1a807ac282c15142933d3a77ccb4bef2f8">set\_auto\_mode\_period</a>

```cpp
uint8_t RollerDrive::set_auto_mode_period (
    uint32_t period_ms
)
```


Auto mode changes poster after some time. Set this time in miliseconds. 

### function <a id="1a6f6648a530348374af71d03727241937" href="#1a6f6648a530348374af71d03727241937">set\_auto\_mode\_range</a>

```cpp
uint8_t RollerDrive::set_auto_mode_range (
    uint8_t from,
    uint8_t to
)
```


Set auto mode range, ie roll from poster 'start' to poster 'to' and repeat. 

### function <a id="1a3813a295ef72fa6e6178871106865c12" href="#1a3813a295ef72fa6e6178871106865c12">calibration</a>

```cpp
uint8_t RollerDrive::calibration (
    void 
)
```


Init and start calibration. 

### function <a id="1ad38a994acf76e19cf7e82cb271a263f6" href="#1ad38a994acf76e19cf7e82cb271a263f6">is\_calibrated</a>

```cpp
bool RollerDrive::is_calibrated (
    void 
)
```


Was calibration successfully finished? 

### function <a id="1a7eb6ce4ec43e09ca43cd3a9c5aba063f" href="#1a7eb6ce4ec43e09ca43cd3a9c5aba063f">get\_poster\_count</a>

```cpp
uint8_t RollerDrive::get_poster_count (
    void 
)
```


Returns number of posters. Return zero if calibration wasn't finished. 

### function <a id="1af02f027daafbc3b6f667b979648b5cf0" href="#1af02f027daafbc3b6f667b979648b5cf0">run\_ind\_motors\_up</a>

```cpp
uint8_t RollerDrive::run_ind_motors_up (
    bool top = false,
    bool bottom = false
)
```



### function <a id="1a241b6e3c6e2f5c45fe44621aec32ce5e" href="#1a241b6e3c6e2f5c45fe44621aec32ce5e">run\_ind\_motors\_down</a>

```cpp
uint8_t RollerDrive::run_ind_motors_down (
    bool top = false,
    bool bottom = false
)
```



### function <a id="1a024f0ec86ffc0790be499f3431415245" href="#1a024f0ec86ffc0790be499f3431415245">run\_ind\_motors\_stop</a>

```cpp
uint8_t RollerDrive::run_ind_motors_stop ()
```



### function <a id="1abdf8cf265ca01a0975f5cf4a2e05c121" href="#1abdf8cf265ca01a0975f5cf4a2e05c121">test\_get\_state\_now</a>

```cpp
uint32_t RollerDrive::test_get_state_now (
    void 
)
```



### function <a id="1adbe96fee8c0882084ddd2ed6f0c0daec" href="#1adbe96fee8c0882084ddd2ed6f0c0daec">test\_get\_state\_last</a>

```cpp
uint32_t RollerDrive::test_get_state_last (
    void 
)
```



### function <a id="1abd808c999d69d9d1d3ef76dfd2bfdc4e" href="#1abd808c999d69d9d1d3ef76dfd2bfdc4e">test\_set\_event</a>

```cpp
void RollerDrive::test_set_event (
    uint32_t event
)
```



### function <a id="1a416e676d5b72714ff5ce87a31f19f653" href="#1a416e676d5b72714ff5ce87a31f19f653">test\_rele</a>

```cpp
void RollerDrive::test_rele (
    uint8_t val
)
```


Test function. Test rele function. 

### function <a id="1aaf762b739d1de55cc4c0db786dcbff69" href="#1aaf762b739d1de55cc4c0db786dcbff69">test\_io</a>

```cpp
void RollerDrive::test_io (
    void 
)
```


Debug function. Read and print all IOs. 



----------------------------------------
The documentation for this class was generated from the following file: `D:/w/hw-libs/\_libs\_/libraries/RollerDrive.h`
