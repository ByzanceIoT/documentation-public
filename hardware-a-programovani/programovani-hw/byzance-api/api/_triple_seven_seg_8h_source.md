---
search: false
---

# TripleSevenSeg.h File Reference

**[Go to the documentation of this file.](_triple_seven_seg_8h.md)**
Source: `D:/w/hw-libs/\_libs\_/libraries/TripleSevenSeg.h`

    
    
    
    
    
    
    
    
    
      
    
    
    
```cpp
/*
 * TrippleSevenSeg.h
 *
 *  Created on: 17. 10. 2017
 *      Author: Viktor
 */

#ifndef LIBRARIES_TRIPPLESEVENSEG_H_
#define LIBRARIES_TRIPPLESEVENSEG_H_

#include "mbed.h"
#include "TCA6424A.h"

#include "byzance_debug.h"
#include "ByzanceLogger.h"

#define SEG_A       (0x01 << 3)
#define SEG_B       (0x01 << 1)
#define SEG_C       (0x01 << 2)
#define SEG_D       (0x01 << 6)
#define SEG_E       (0x01 << 7)
#define SEG_F       (0x01 << 5)
#define SEG_G       (0x01 << 4)
#define SEG_DP      (0x01 << 0)

class TripleSevenSeg {
    public:
        TripleSevenSeg();

        bool is_initialized(void);

        bool display_number(float value, uint8_t decimal_positions);

        uint32_t display_symbol(char symbol, uint8_t position, bool dot);
    protected:


    private:
        TCA6424A * _driver;
        bool _initialized;
};



#endif /* LIBRARIES_TRIPLESEVENSEG_H_ */
```


    
  
