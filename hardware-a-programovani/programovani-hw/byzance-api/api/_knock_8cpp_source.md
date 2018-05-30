---
search: false
---

# Knock.cpp File Reference

**[Go to the documentation of this file.](_knock_8cpp.md)**
Source: `D:/w/hw-libs/\_libs\_/libraries/Knock.cpp`

    
    
    
      
    
    
    
```cpp
#include "Knock.h"

REGISTER_DEBUG(Knock);

Knock::Knock(PinName acc_sda, PinName acc_scl, PinName mic):
    _acc(acc_sda, acc_scl),
    _mic(mic)
{

    _acc.set_Ascale(AFS_2G);
    _acc.set_Gscale(GFS_250DPS);

    _offset_acc = 0.800;
    _offset_mic = 0.350;

    _coef_acc   = 0.625;
    _coef_mic   = 2.222;

    _stage = KNOCK_STAGE_WAITING;

    _thread = new Thread(osPriorityLow, 2048);

}

Knock::~Knock(){

}

void Knock::start(){
    _thread->start(callback(this, &Knock::thread_func));
}

void Knock::stop(){
    _thread->terminate();
}

int Knock::read_raw_acc(float* val){

    _acc.update_motion();
    *val = sqrt(pow(_acc.ax, 2) + pow(_acc.ay, 2) + pow(_acc.az, 2));

    // todo: return some code if read failed

    return 0;

}

int Knock::read_raw_mic(float* val){

    *val = _mic.read();

    // todo: return some code if read failed
    return 0;
}

int Knock::set_acc_calibration(float offset, float coef){

    // TODO: filter obviously invalid params

    _offset_acc = offset;
    _coef_acc   = coef;

    return 0;
}

int Knock::set_mic_calibration(float offset, float coef){

    // TODO: filter obviously invalid params

    _offset_mic = offset;
    _coef_mic   = coef;

    return 0;
}

void Knock::thread_func(){

    // current values
    float acc_val = 0;
    float mic_val = 0;

    // maximum values
    float acc_max = 0;
    float mic_max = 0;

    bool state_acc_previous = false;
    bool state_mic_previous = false;

    bool state_both_previous = false;

    Timer t;
    t.start();

    Timer tim;
    tim.start();

    sensor_event_t event = SENSOR_EVENT_NONE;

    while(1){

        /*
         * MEASURE DATA
         */
        read_raw_acc(&acc_val);
        read_raw_mic(&mic_val);


        /*
         * STORE DATA
         */
        // shift acc values to the right
        for(int i = NUMBER_OF_SAMPLES - 2; i >= 0; i--){
            _acc_window[i + 1] = _acc_window[i];
        }

        // shift mic values to the right
        for(int i = NUMBER_OF_SAMPLES - 2; i >= 0; i--){
            _mic_window[i + 1] = _mic_window[i];
        }

        // remove offset and normalize
        // add new values to the left
        _acc_window[0] = (acc_val-_offset_acc)*_coef_acc;
        _mic_window[0] = (mic_val-_offset_mic)*_coef_mic;

        __TRACE("acc_val = %f, mic_val = %f\n", acc_val, mic_val);

        acc_max = find_maximum(_acc_window);

        __TRACE("acc_array\n");
        for(uint32_t i = 0; i<NUMBER_OF_SAMPLES; i++){
            __TRACE("- %f\n", _acc_window[i]);
        }
        __DEBUG("acc -> max = %f\n", acc_max);


        mic_max = find_maximum(_mic_window);

        __TRACE("mic_array\n");
        for(uint32_t i = 0; i<NUMBER_OF_SAMPLES; i++){
            __TRACE("- %f\n", _mic_window[i]);
        }
        __DEBUG("mic -> max = %f\n", mic_max);

#ifdef NECHCI
        /*
         * ACCELEROMETER
         */
        if(acc_max > ACC_THRESHOLD){

            _state_acc = true;

            // current state high, previous state low
            // mic rise edge
            if(!state_acc_previous){
                __DEBUG("ACC RISE\n");
            }

        } else {

            _state_acc = false;

            // current state low, previous state high
            // fall edge
            if(state_acc_previous){
                __DEBUG("ACC FALL\n");
            }

        }

        state_acc_previous = _state_acc;

        /*
         * MICROPHONE
         */
        if(mic_max > MIC_THRESHOLD){

            _state_mic = true;

            // current state high, previous state low
            // mic rise edge
            if(!state_mic_previous){
                __DEBUG("MIC RISE\n");
            }

        } else {

            _state_mic = false;

            // current state low, previous state high
            // fall edge
            if(state_mic_previous){
                __DEBUG("MIC FALL\n");
            }

        }

        state_mic_previous = _state_mic;

        /*
         * BOTH SENSORS TOGETHER
         */
        if(_state_acc && _state_mic){

            _state_both = true;

            // both current state high, previous state low
            // rise edge
            if(!state_both_previous){
                __DEBUG("BOTH RISE; t = %d ms\n", t.read_ms());
                event = SENSOR_EVENT_RISE;
                t.reset();
            }

        } else {

            _state_both = false;

            // some of them low, previously both high
            if(state_both_previous){
                __DEBUG("SOME OF SENSORS DOWN; t = %d ms\n", t.read_ms());
                event = SENSOR_EVENT_FALL;
                t.reset();
            }

        }
#endif

        /*
         * BOTH SENSORS TOGETHER - new
         */
        if((acc_max + mic_max)>1){

            _state_both = true;

            // both current state high, previous state low
            // rise edge
            if(!state_both_previous){
                __DEBUG("BOTH RISE; t = %d ms\n", t.read_ms());
                event = SENSOR_EVENT_RISE;
                t.reset();
            }

        } else {

            _state_both = false;

            // some of them low, previously both high
            if(state_both_previous){
                __DEBUG("SOME OF SENSORS DOWN; t = %d ms\n", t.read_ms());
                event = SENSOR_EVENT_FALL;
                t.reset();
            }

        }



        /*
         * STATE MACHINE
         */

        // stage 1
        // waiting for peak
        if(_stage == KNOCK_STAGE_WAITING){

            // both sensors rise event
            if(event == SENSOR_EVENT_RISE){

                // time was LONG enough (which is good) -> switch to the next stage
                if(tim.read_ms()>TIME_WAITING){
                    _stage = KNOCK_STAGE_PEAK;
                    __WARNING("(STAGE 1) SWITCHING 1->2, time was = %d\n", tim.read_ms());

                // time was TOO SHORT -> reset stage 1
                } else {
                    _stage = KNOCK_STAGE_WAITING;
                    __WARNING("(STAGE 1) RESET, time was = %d\n", tim.read_ms());
                }

                tim.reset();
            }
        }

        if(_stage == KNOCK_STAGE_PEAK){

            // both sensors fall event
            if(event == SENSOR_EVENT_FALL){

                // time is SHORT enough (which is good, because there was short peak) -> switch to the next stage
                if(tim.read_ms()<TIME_PEAK){

                    _stage = KNOCK_STAGE_AFTER;
                    __WARNING("(STAGE 2) SWITCHING 2->3, time was = %d\n", tim.read_ms());

                // time was TOO LONG (probably some long noise) -> return to the stage 1
                } else {
                    _stage = KNOCK_STAGE_WAITING;
                    __WARNING("(STAGE 2) TOO LONG PEAK -> SWITCHED 2->1, time was = %d\n", tim.read_ms());
                }

                tim.reset();
            }
        }


        if(_stage == KNOCK_STAGE_AFTER){

            if(event == SENSOR_EVENT_RISE){

                __WARNING("(STAGE 3) too fast rise interrupt -> switching STAGE 3->1\n");
                _stage = KNOCK_STAGE_WAITING;
                tim.reset();

            } else {

                // time was long enough
                if(tim.read_ms()>TIME_AFTER){

                    __WARNING("(STAGE 3) FINAL STAGE FINISHED, time was = %d\n", tim.read_ms());

                    __WARNING("(STAGE 3) CALLING CALLBACK + SWITCHING STAGE 3->1\n");

                    // call callback
                    if(_knock_callback){
                        _knock_callback.call();
                    }

                    _stage = KNOCK_STAGE_WAITING;


                    tim.reset();

                }

            }

        }

        state_both_previous = _state_both;

        event = SENSOR_EVENT_NONE;

        __TRACE("****************************************\n");

        Thread::wait(1);
    }

}

float Knock::find_maximum(float* array){

    float max = 0;

    for(uint32_t i = 0; i<NUMBER_OF_SAMPLES; i++){
        if(array[i] > max){
            max = array[i];
        }
    }

    return max;
}

void Knock::attach_knock_detection(void (*function)(void)) {
    _knock_callback = callback(function);
}
```


    
  
