---
search: false
---

# WakeUp.h File Reference

**[Go to the documentation of this file.](_wake_up_8h.md)**
Source: `D:/w/hw-libs/\_libs\_/libraries/WakeUp.h`

    
    
    
    
    
    
    
```cpp
#include "mbed.h"

class WakeUp
{
public:
    static void set(uint32_t s) {
        set_ms(1000 * s);
    }
    
    static void set_ms(uint32_t ms);
    
    static void attach(Callback<void()> function) {
        callback = function;
    }
    
    static void calibrate(void);


private:
    static Callback<void()> callback;
    static void irq_handler(void);
    static float cycles_per_ms;
};
```


    
  
