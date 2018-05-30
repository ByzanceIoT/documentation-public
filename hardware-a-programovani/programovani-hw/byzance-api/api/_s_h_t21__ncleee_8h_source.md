---
search: false
---

# SHT21\_ncleee.h File Reference

**[Go to the documentation of this file.](_s_h_t21__ncleee_8h.md)**
Source: `D:/w/hw-libs/\_libs\_/libraries/SHT21\_ncleee.h`

    
    
    
    
    
    
    
    
      
    
    
    
```cpp
/* Copyright (c) 2012 Graeme Coapes, Newcastle University, MIT License
 *
 * Permission is hereby granted, free of charge, to any person obtaining a copy of this software 
 * and associated documentation files (the "Software"), to deal in the Software without restriction, 
 * including without limitation the rights to use, copy, modify, merge, publish, distribute, 
 * sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is 
 * furnished to do so, subject to the following conditions:
 *
 * The above copyright notice and this permission notice shall be included in all copies or 
 * substantial portions of the Software.
 *
 * THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING 
 * BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND 
 * NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, 
 * DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, 
 * OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
 */


#include "mbed.h"

#include "ByzanceLogger.h"
#include "byzance_debug.h"

#ifndef SHT21_ncleee
#define SHT21_ncleee

    /*
     * Constants used in communication
     *
     * Refer to datasheet for full explanation
     */ 
     
    //Sensor I2C address
    #define SHT_I2C_ADDR        0x80
    
    //Commands...
    //Trigger Temp with hold master
    #define SHT_TRIG_TEMP_HOLD  0xE3
    //Trigger RH with hold master
    #define SHT_TRIG_RH_HOLD    0xE5
    //Trigger Temp with no hold master
    #define SHT_TRIG_TEMP       0xF3
    //Trigger RH with no hold master
    #define SHT_TRIG_RH         0xF5
    //Write to user register
    #define SHT_WRITE_REG       0xE6
    //Read from user register
    #define SHT_READ_REG        0xE7
    //Soft reset the sensor
    #define SHT_SOFT_RESET      0xFE
    
    //User Register information
    
    //Data precision settings
    //RH 12 T 14 - default
    #define SHT_PREC_1214       0x00
    //RH 8  T 10 
    #define SHT_PREC_0812       0x01
    //RH 10 T 13
    #define SHT_PREC_1013       0x80
    //RH 11 T 11
    #define SHT_PREC_1111       0x81

    //Battery status
    #define SHT_BATTERY_STAT    0x40
    //Enable on chip heater
    #define SHT_HEATER          0x04
    //Disable OTP reload
    #define SHT_DISABLE_OTP     0x02
    
    
    //Fail conditions on the I2C bus
    #define SHT_FAIL            1
    #define SHT_SUCCESS         0
    
    //Author fail conditions
    //1, 2, 3 can be used because these are status bits
    //in the received measurement value
    #define SHT_GOOD            0xFFFC
    #define SHT_TRIG_FAIL       1
    #define SHT_READ_FAIL       2
    
    class SHT21
    {
        private:
            I2C *_i2c;
//            Serial *_pc;
            float _temp = -280;
            float _hum = -1;
            int triggerTemp();  
            int requestTemp();
            unsigned short temperature;
            int triggerRH();
            int requestRH();
            unsigned short humidity;
            int wr(int cmd);
            
        public:
        
            SHT21(I2C *i2c);
            
            float readTemp();
            
            float readHumidity();
            
            int reset();
            
            int setPrecision(char precision);
    
    };
    
    
#endif
```


    
  
