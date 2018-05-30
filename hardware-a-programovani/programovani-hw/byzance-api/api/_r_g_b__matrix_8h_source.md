---
search: false
---

# RGB\_matrix.h File Reference

**[Go to the documentation of this file.](_r_g_b__matrix_8h.md)**
Source: `D:/w/hw-libs/\_libs\_/libraries/RGB\_matrix.h`

    
    
    
    
    
    
    
    
      
    
    
    
```cpp
/*
 * RGB_matrix.h
 *
 *  Created on: 28. 11. 2017
 *      Author: David Kopecký
 */

#ifndef RGB_MATRIX_H_
#define RGB_MATRIX_H_

#include "mbed.h"
#include "HD44780_6x8.h"
#include <string>
//#include <iostream>

enum RGB_MATRIX_COLOR {
    NONE = 0,
    BLUE,
    GREEN,
    LIGHT_BLUE,
    RED,
    PINK,
    YELLOW,
    WHITE
};




class RGB_matrix{


    public:

    static void Init(PinName Pin_R1, PinName Pin_R2,PinName Pin_G1 ,PinName Pin_G2, PinName Pin_B1,PinName Pin_B2,
            PinName Pin_CLK,PinName Pin_LAT, PinName Pin_OE, PinName Pin_A,PinName Pin_B,PinName Pin_C,PinName Pin_D);

    static void set_color(char color);

    static void set_background(char color);

    static void set_pixel(uint16_t x ,uint16_t y, uint16_t c);

    static char put_char(int x,int y, char c);

    static void put_line(char* str, int line_number);


    static void put_row(char* str,uint16_t mins, int line_number);

    static void paint();

    static void paint_all();

    static void detach_ticker();

    static void attach_ticker();



    private:

    static BusOut* ABCD; // Row address.
    static DigitalOut* CLK;    //  Data clock    - rising edge
    static DigitalOut* LAT;    //  Data latch    - active low (pulse up after data load)
    static DigitalOut* OE;     //  Output enable - active low (hold high during data load, bring low after LAT pulse)
    static DigitalOut* R1;     //  RED   Serial in for upper half
    static DigitalOut* R2;     //  RED   Serial in for lower half
    static DigitalOut* G1;      //  GREEN Serial in for upper half
    static DigitalOut* G2;      //  GREEN Serial in for lower half
    static DigitalOut* B1;      //  BLUE  Serial in for upper half
    static DigitalOut* B2;      //  BLUE  Serial in for lower half

    static Ticker*  painter;

    static uint16_t row_cnt;
    static uint16_t cycle_cnt;
    static uint16_t gm[128][6]; // Buffer with 128*6*16 bits. Graphics memory if you like.
    static char _background;
    static char _color;

    /*
     * Vykreslý zadaný øádek na display
     * \param Row - èíslo øádku
     */
    static void write_row(uint16_t Row);



};

#endif /* RGB_MATRIX_H_ */

```


    
  
