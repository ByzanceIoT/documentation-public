---
search: false
---

# TLC59116.h File Reference

**[Go to the documentation of this file.](_t_l_c59116_8h.md)**
Source: `D:/w/hw-libs/\_libs\_/libraries/TLC59116.h`

    
    
    
    
    
    
    
    
      
    
    
    
```cpp
/*
 * TLC59116.h
 *
 *  Created on: 18. 10. 2017
 *      Author: Viktor
 */

#ifndef TLC59116_H_
#define TLC59116_H_


#include "mbed.h"

#include "byzance_debug.h"
#include "ByzanceLogger.h"

// I2C address on ShieldB1L_LED_170920
#define TLC59116_DEFAULT_ADDRESS        ((uint8_t)0b11011110)

// Register definitions in TLC59116 driver
#define TLC59116_ALLCALL    0b11010000
#define TLC59116_SUB1       0b11010010
#define TLC59116_SUB2       0b11010100
#define TLC59116_SUB3       0b11011000
#define TLC59116_RESET      0b11010110

#define TLC59116_MODE1      0x00
#define TLC59116_MODE2      0x01
#define TLC59116_PWM0       0x02
#define TLC59116_PWM1       0x03
#define TLC59116_PWM2       0x04
#define TLC59116_PWM3       0x05
#define TLC59116_PWM4       0x06
#define TLC59116_PWM5       0x07
#define TLC59116_PWM6       0x08
#define TLC59116_PWM7       0x09
#define TLC59116_PWM8       0x0A
#define TLC59116_PWM9       0x0B
#define TLC59116_PWM10      0x0C
#define TLC59116_PWM11      0x0D
#define TLC59116_PWM12      0x0E
#define TLC59116_PWM13      0x0F
#define TLC59116_PWM14      0x10
#define TLC59116_PWM15      0x11
#define TLC59116_GRPPWM     0x12
#define TLC59116_GRPFREQ    0x13
#define TLC59116_LEDOUT0    0x14
#define TLC59116_LEDOUT1    0x15
#define TLC59116_LEDOUT2    0x16
#define TLC59116_LEDOUT3    0x17
#define TLC59116_SUBADR1    0x18
#define TLC59116_SUBADR2    0x19
#define TLC59116_SUBADR3    0x1A
#define TLC59116_ALLCALLADR 0x1B
#define TLC59116_IREF       0x1C
#define TLC59116_EFLAG1     0x1D
#define TLC59116_EFLAG2     0x1E

class TLC59116 {
    public:

        TLC59116();

        uint8_t initialize(PinName sda, PinName scl);

        uint8_t reset_sw(void);

        uint8_t set_channel(uint8_t channel, uint8_t pwm);

        uint8_t set_all_channels(uint8_t * data);

        uint8_t set_register(uint8_t reg, uint8_t value);

        uint8_t set_global_pwm(uint8_t pwm);

    private:
        uint8_t _addr;
        I2C*    _i2c;
        bool _initialized;


};


#endif /* TLC59116_H_ */
```


    
  
