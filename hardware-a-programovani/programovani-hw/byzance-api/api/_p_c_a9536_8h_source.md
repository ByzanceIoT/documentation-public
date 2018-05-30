---
search: false
---

# PCA9536.h File Reference

**[Go to the documentation of this file.](_p_c_a9536_8h.md)**
Source: `D:/w/hw-libs/\_libs\_/libraries/PCA9536.h`

    
    
    
    
    
    
    
    
    
      
    
    
    
```cpp
/*
 * PCA9536.h
 *
 *  Created on: 18. 10. 2017
 *      Author: martin
 */

#ifndef PCA9536_H_
#define PCA9536_H_

#include "mbed.h"
#include "byzance_debug.h"
#include "ByzanceLogger.h"

#define PCA9536_ADDR                0x82

#define PCA9536_PINS                4

#define PCA9536_REG_INPUT           0x00
#define PCA9536_REG_OUTPUT          0x01
#define PCA9536_REG_POLARITY        0x02
#define PCA9536_REG_CONFIGURATION   0x03


class PCA9536{
    public:
        PCA9536(PinName sda, PinName scl);

        /*
         * all funtions has the same return codes
         *
         *  0       OK
         * -2       invalid pin
         * other    inherted from I2C library
         */

        int set_all_inputs();

        int set_all_outputs();

        int set_output(uint8_t pin);

        int set_input(uint8_t pin);

        int set_value(uint8_t value);

        int set_value(uint8_t pin, uint8_t value);

        int get_value(uint8_t *value);

        int get_value(uint8_t pin, uint8_t *value);
    protected:
        I2C     _i2c;

        //write val to reg
        int _write_reg(uint8_t reg, uint8_t val);

        //read val from reg
        int _read_reg(uint8_t reg, uint8_t *val);
};


#endif /* PCA9536_H_ */
```


    
  
