---
search:
  keywords:
    - Knock
    - _acc
    - _mic
    - _tick
    - _thread
    - _acc_window
    - _mic_window
    - _state_mic
    - _state_acc
    - _state_both
    - _stage
    - _offset_acc
    - _offset_mic
    - _coef_acc
    - _coef_mic
    - _knock_callback
    - Knock
    - ~Knock
    - start
    - stop
    - read_raw_acc
    - read_raw_mic
    - set_acc_calibration
    - set_mic_calibration
    - attach_knock_detection
    - attach_knock_detection
    - thread_func
    - find_maximum
---

# Knock

TO DO. [More...](knock.md#detailed-description)

## Protected Attributes

| Type | Name |
| :--- | :--- |
| [**MPU9150**](mpu9150.md) | [**\_acc**](knock.md#1a1e4179879eb927650c2b6f8b9519ecc2) |
| AnalogIn | [**\_mic**](knock.md#1a41524e28d2983cca57491cb55a577990) |
| Ticker | [**\_tick**](knock.md#1afc79153e9cda52057e7b26eb844d62c6) |
| Thread \* | [**\_thread**](knock.md#1af22b68b9fb25a2f8c8b2d285cdff30e8) |
| float | [**\_acc\_window**](knock.md#1a58637f62c065ba4328753de4f474d52b) |
| float | [**\_mic\_window**](knock.md#1a0958f0e8be1964be5fd5f07d69c35b69) |
| bool | [**\_state\_mic**](knock.md#1a7c4adc36fe769d78553d6d98277b9d72) |
| bool | [**\_state\_acc**](knock.md#1ab0e3b108fae3a767f3bb19ac3636519d) |
| bool | [**\_state\_both**](knock.md#1a50cc06212961949c29d4de0463606779) |
| knock\_stage\_t | [**\_stage**](knock.md#1ad454c9e1acb7ae09171f1b261b3a8bbb) |
| float | [**\_offset\_acc**](knock.md#1ac929ed20f058166c908de984823b7c50) |
| float | [**\_offset\_mic**](knock.md#1a74f1df4bf2c549b797487fb0458449a9) |
| float | [**\_coef\_acc**](knock.md#1a011f42175488a699f86f2d9ff6910ce9) |
| float | [**\_coef\_mic**](knock.md#1a7627b2e435fc091ca3d03dd8d844598a) |
| Callback&lt; void\(void\)&gt; | [**\_knock\_callback**](knock.md#1a998db70cb8bf07ecf68974c702e299ee) |

## Public Functions

| Type | Name |
| :--- | :--- |
|  | [**Knock**](knock.md#1ab6e36d4711fa31772bc0f86b1e9c8519) \(PinName acc\_sda, PinName acc\_scl, PinName mic\) |
|  | [**~Knock**](knock.md#1ac2755a23c5b160f6032c7634d1e63204) \(\) |
| void | [**start**](knock.md#1a874f3ecfaadceeaa6bb62e7949e6dda4) \(\) |
| void | [**stop**](knock.md#1aed85e4119b9292d79b1bf2a7f27ed50f) \(\) |
| int | [**read\_raw\_acc**](knock.md#1a8c6342fe284daf1f5440b1e3a31a5f35) \(float \* val\) |
| int | [**read\_raw\_mic**](knock.md#1af335b3220e28dda4b048474ae7ab7093) \(float \* val\) |
| int | [**set\_acc\_calibration**](knock.md#1a0c76f8aa85b369baf401be6cc5290b24) \(float offset, float coef\) |
| int | [**set\_mic\_calibration**](knock.md#1a87e55f9d265fb802201d817f06a269b5) \(float offset, float coef\) |
| void | [**attach\_knock\_detection**](knock.md#1a3c25f5676a659856fdd4af6b22a01f23) \(void\(\*\)\(void\) function\) |
| void | [**attach\_knock\_detection**](knock.md#1a3b7f6c5453b315ccf678095d6f8e797a) \(T \* object, void\(T::\*\)\(void\) member\) |

## Protected Functions

| Type | Name |
| :--- | :--- |
| void | [**thread\_func**](knock.md#1a5f2e9f99fe152302297c403c25e18256) \(\) |
| float | [**find\_maximum**](knock.md#1afc8ddfe75827b68a37b8c8cf93189c68) \(float \* array\) |

## Detailed Description

description TO DO.

## Protected Attributes Documentation

### variable [\_acc](knock.md#1a1e4179879eb927650c2b6f8b9519ecc2)

```cpp
MPU9150 Knock::_acc;
```

### variable [\_mic](knock.md#1a41524e28d2983cca57491cb55a577990)

```cpp
AnalogIn Knock::_mic;
```

### variable [\_tick](knock.md#1afc79153e9cda52057e7b26eb844d62c6)

```cpp
Ticker Knock::_tick;
```

### variable [\_thread](knock.md#1af22b68b9fb25a2f8c8b2d285cdff30e8)

```cpp
Thread* Knock::_thread;
```

### variable [\_acc\_window](knock.md#1a58637f62c065ba4328753de4f474d52b)

```cpp
float Knock::_acc_window[NUMBER_OF_SAMPLES];
```

### variable [\_mic\_window](knock.md#1a0958f0e8be1964be5fd5f07d69c35b69)

```cpp
float Knock::_mic_window[NUMBER_OF_SAMPLES];
```

### variable [\_state\_mic](knock.md#1a7c4adc36fe769d78553d6d98277b9d72)

```cpp
bool Knock::_state_mic;
```

### variable [\_state\_acc](knock.md#1ab0e3b108fae3a767f3bb19ac3636519d)

```cpp
bool Knock::_state_acc;
```

### variable [\_state\_both](knock.md#1a50cc06212961949c29d4de0463606779)

```cpp
bool Knock::_state_both;
```

### variable [\_stage](knock.md#1ad454c9e1acb7ae09171f1b261b3a8bbb)

```cpp
knock_stage_t Knock::_stage;
```

### variable [\_offset\_acc](knock.md#1ac929ed20f058166c908de984823b7c50)

```cpp
float Knock::_offset_acc;
```

### variable [\_offset\_mic](knock.md#1a74f1df4bf2c549b797487fb0458449a9)

```cpp
float Knock::_offset_mic;
```

### variable [\_coef\_acc](knock.md#1a011f42175488a699f86f2d9ff6910ce9)

```cpp
float Knock::_coef_acc;
```

### variable [\_coef\_mic](knock.md#1a7627b2e435fc091ca3d03dd8d844598a)

```cpp
float Knock::_coef_mic;
```

### variable [\_knock\_callback](knock.md#1a998db70cb8bf07ecf68974c702e299ee)

```cpp
Callback<void(void)> Knock::_knock_callback;
```

## Public Functions Documentation

### function [Knock](knock.md#1ab6e36d4711fa31772bc0f86b1e9c8519)

```cpp
Knock::Knock (
    PinName acc_sda,
    PinName acc_scl,
    PinName mic
)
```

### function [~Knock](knock.md#1ac2755a23c5b160f6032c7634d1e63204)

```cpp
Knock::~Knock ()
```

### function [start](knock.md#1a874f3ecfaadceeaa6bb62e7949e6dda4)

```cpp
void Knock::start ()
```

### function [stop](knock.md#1aed85e4119b9292d79b1bf2a7f27ed50f)

```cpp
void Knock::stop ()
```

### function [read\_raw\_acc](knock.md#1a8c6342fe284daf1f5440b1e3a31a5f35)

```cpp
int Knock::read_raw_acc (
    float * val
)
```

### function [read\_raw\_mic](knock.md#1af335b3220e28dda4b048474ae7ab7093)

```cpp
int Knock::read_raw_mic (
    float * val
)
```

### function [set\_acc\_calibration](knock.md#1a0c76f8aa85b369baf401be6cc5290b24)

```cpp
int Knock::set_acc_calibration (
    float offset,
    float coef
)
```

### function [set\_mic\_calibration](knock.md#1a87e55f9d265fb802201d817f06a269b5)

```cpp
int Knock::set_mic_calibration (
    float offset,
    float coef
)
```

### function [attach\_knock\_detection](knock.md#1a3c25f5676a659856fdd4af6b22a01f23)

```cpp
void Knock::attach_knock_detection (
    void(*)(void) function
)
```

### function [attach\_knock\_detection](knock.md#1a3b7f6c5453b315ccf678095d6f8e797a)

```cpp
void Knock::attach_knock_detection (
    T * object,
    void(T::*)(void) member
)
```

## Protected Functions Documentation

### function [thread\_func](knock.md#1a5f2e9f99fe152302297c403c25e18256)

```cpp
void Knock::thread_func ()
```

### function [find\_maximum](knock.md#1afc8ddfe75827b68a37b8c8cf93189c68)

```cpp
float Knock::find_maximum (
    float * array
)
```

The documentation for this class was generated from the following file: `D:/w/hw-libs/\_libs\_/libraries/Knock.h`

