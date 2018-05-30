---
search: false
---

# Knock.h File Reference

**[Go to the documentation of this file.](_knock_8h.md)**
Source: `D:/w/hw-libs/\_libs\_/libraries/Knock.h`

    
    
    
    
    
    
    
    
      
      
    
    
    
```cpp
#ifndef KNOCK_H_
#define KNOCK_H_

#include "ByzanceLogger.h"
#include "byzance_debug.h"

#include "MPU9150.h"

#define NUMBER_OF_SAMPLES   16
#define ACC_THRESHOLD       1.5
#define MIC_THRESHOLD       0.6

// minimum waiting delay
#define TIME_WAITING        300

// maximum peak time
#define TIME_PEAK           250

// maximum peak time
#define TIME_AFTER          300

typedef enum : unsigned char {
    KNOCK_STAGE_WAITING,
    KNOCK_STAGE_PEAK,
    KNOCK_STAGE_AFTER,
} knock_stage_t;

typedef enum : unsigned char {
    SENSOR_EVENT_NONE,
    SENSOR_EVENT_RISE,
    SENSOR_EVENT_FALL,
} sensor_event_t;

class Knock {

    public:    
  
        Knock(PinName acc_sda, PinName acc_scl, PinName mic);
        ~Knock();

        void start();
        void stop();

        int read_raw_acc(float* val);
        int read_raw_mic(float* val);

        int set_acc_calibration(float offset, float coef);
        int set_mic_calibration(float offset, float coef);

        void attach_knock_detection(void (*function)(void));

        template<typename T>
        void attach_knock_detection(T *object, void (T::*member)(void)) {
            _knock_callback.attach(object, member);
        }

    protected:

        void thread_func();

        float find_maximum(float* array);

        // accelerometer
        MPU9150     _acc;

        // microphone
        AnalogIn    _mic;

        Ticker      _tick;

        Thread*     _thread;

        float   _acc_window[NUMBER_OF_SAMPLES];
        float   _mic_window[NUMBER_OF_SAMPLES];

        bool    _state_mic = false;
        bool    _state_acc = false;

        bool    _state_both = false;

        knock_stage_t _stage;

        float   _offset_acc;
        float   _offset_mic;

        float   _coef_acc;
        float   _coef_mic;

        Callback<void(void)>    _knock_callback;

    private:

};

#endif /* KNOCK_H_ */
```


    
  
