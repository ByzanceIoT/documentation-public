---
search: false
---

# DS1820.cpp File Reference

**[Go to the documentation of this file.](_d_s1820_8cpp.md)**
Source: `D:/w/hw-libs/\_libs\_/libraries/DS1820.cpp`

    
    
    
      
      
    
    
    
```cpp
/*
 * Dallas' DS1820 family temperature sensor.
 * This library depends on the OneWire library (Dallas' 1-Wire bus protocol implementation)
 * available at <http://developer.mbed.org/users/hudakz/code/OneWire/>
 *
 * Example of use:
 * 
 * #include "DS1820.h"
 *
 * Serial serial(USBTX, USBRX);
 * 
 * int main() {
 *     DS1820  ds1820(PA_9);    // substitute PA_9 with actual mbed pin name connected to the DS1820 data pin
 *
 *     if(ds1820.begin()) {
 *        ds1820.startConversion();
 *        wait(1.0);
 *        while(1) {
 *            printf("temp = %3.1f\r\n", ds1820.read());     // read temperature
 *            ds1820.startConversion();     // start temperature conversion
 *            wait(1.0);                    // let DS1820 complete the temperature conversion
 *        }
 *    } else
 *        printf("No DS1820 sensor found!\r\n");
 * }
 *
 * 
 * Note: Don't forget to connect a 4.7k Ohm resistor 
 *       between the DS1820's data pin and the +3.3V pin
 *
 */
 
#include "DS1820.h"

#define DEBUG 0

REGISTER_DEBUG(DS1820);


DS1820::DS1820(PinName pin) :
    oneWire(pin) {
    present = false;
    model_s = false;
}

DS1820::DS1820(char model, PinName pin) :
    oneWire(pin) {
    if((model == 'S') or (model == 's')) {
        present = true;
        model_s = true;
    }
    else if((model == 'B') or (model == 'b')) {
        present = true;
        model_s = false;
    }
    else
        present = false;
}

bool DS1820::begin(void) {
    oneWire.reset_search();
    wait_ms(250);
    if(!oneWire.search(addr)) {
        __DEBUG("No addresses.\r\n");

        oneWire.reset_search();
        wait_ms(250);
        return false;
    }

    // Debug print obly
    __DEBUG("ROM =");
    for(uint8_t i = 0; i < 8; i++) {
        __DEBUG(" %x", addr[i]);
    }
    __DEBUG("\r\n");

    if(OneWire::crc8(addr, 7) == addr[7]) {
        present = true;

        // the first ROM byte indicates which chip
        switch(addr[0]) {
        case 0x10:
            model_s = true;
            __DEBUG("DS18S20 or old DS1820\r\n");
            break;

        case 0x28:
            model_s = false;
            __DEBUG("DS18B20\r\n");
            break;

        case 0x22:
            model_s = false;
            __DEBUG("DS1822\r\n");
            break;

        default:
            present = false;
            __DEBUG("Device doesn't belong to the DS1820 family\r\n");
            return false;
        }
        return true;
    }
    else {
        __DEBUG("Invalid CRC!\r\n");
        return false;
    }
}

bool DS1820::isPresent(void) {
    return present;
}

void DS1820::setResolution(uint8_t res) {
    // keep resolution within limits
    if(res > 12)
        res = 12;
    if(res < 9)
        res = 9;      
    if(model_s)
        res = 9;
       
    oneWire.reset();
    oneWire.skip();
    oneWire.write(0xBE);            // to read Scratchpad

    // read Scratchpad bytes
    for(uint8_t i = 0; i < 9; i++){
        data[i] = oneWire.read();
    }

    data[4] |= (res - 9) << 5;      // update configuration byte (set resolution)  
    oneWire.reset();
    oneWire.skip();
    oneWire.write(0x4E);            // to write into Scratchpad

    // write three bytes (2nd, 3rd, 4th) into Scratchpad
    for(uint8_t i = 2; i < 5; i++) {
        oneWire.write(data[i]);
    }
}

void DS1820::startConversion(void) {
    if(present) {
        oneWire.reset();
        oneWire.skip();
        oneWire.write(0x44);    //start temperature conversion
    } else {
        __WARNING("not present\n");
    }
}

float DS1820::read(void) {

    if(present) {

        oneWire.reset();
        oneWire.skip();
        oneWire.write(0xBE);            // to read Scratchpad

        // read Scratchpad bytes
        for(uint8_t i = 0; i < 9; i++){
            data[i] = oneWire.read();
        }

        // Convert the raw bytes to a 16-bit unsigned value
        uint16_t*   p_word = reinterpret_cast < uint16_t * > (&data[0]);

        __DEBUG("raw = %#x\r\n", *p_word);

        if(model_s) {
            *p_word = *p_word << 3;         // 9-bit resolution
            if(data[7] == 0x10) {

                // "count remain" gives full 12-bit resolution
                *p_word = (*p_word & 0xFFF0) + 12 - data[6];
            }
        } else {
            uint8_t cfg = (data[4] & 0x60); // default 12-bit resolution
            
            // at lower resolution, the low bits are undefined, so let's clear them
            if(cfg == 0x00)
                *p_word = *p_word &~7;      //  9-bit resolution
            else
            if(cfg == 0x20)
                *p_word = *p_word &~3;      // 10-bit resolution
            else
            if(cfg == 0x40)
                *p_word = *p_word &~1;      // 11-bit resolution
                                               
        }

        // Convert the raw bytes to a 16-bit signed fixed point value :
        // 1 sign bit, 7 integer bits, 8 fractional bits (two’s compliment
        // and the LSB of the 16-bit binary number represents 1/256th of a unit).
        *p_word = *p_word << 4;
        
        // Convert to floating point value
        return(toFloat(*p_word));
    }

    __WARNING("not present\n");

    return 0;
}

uint8_t DS1820::read(float& temp) {

    if(present) {

        oneWire.reset();
        oneWire.skip();
        oneWire.write(0xBE);

        // to read Scratchpad
        // reading scratchpad registers
        for(uint8_t i = 0; i < 9; i++) {
            data[i] = oneWire.read();
        }

        // if calculated CRC does not match the stored one
        // return with CRC error
        if(oneWire.crc8(data, 8) != data[8]){
            __WARNING("crc fail, disconnecting\n");
            present = 0;
            return 2;
        }

        __DEBUG("crc8 = %d, data8 = %d\n", oneWire.crc8(data, 8), data[8]);

        // Convert the raw bytes to a 16bit unsigned value
        uint16_t*   p_word = reinterpret_cast < uint16_t * > (&data[0]);
        __DEBUG("raw = %#x\r\n", *p_word);

        if(model_s) {

            *p_word = *p_word << 3;         // 9 bit resolution,  max conversion time = 750ms
            if(data[7] == 0x10) {

                // "count remain" gives full 12 bit resolution
                *p_word = (*p_word & 0xFFF0) + 12 - data[6];
            }

            // Convert the raw bytes to a 16bit signed fixed point value :
            // 1 sign bit, 7 integer bits, 8 fractional bits (two's compliment
            // and the LSB of the 16bit binary number represents 1/256th of a unit).
            *p_word = *p_word << 4;
            // Convert to floating point value
            temp = toFloat(*p_word);

            __WARNING("s - read with no errors\n");

            return 0;   // return with no errors

        } else {

            uint8_t cfg = (data[4] & 0x60); // default 12bit resolution, max conversion time = 750ms

            // at lower resolution, the low bits are undefined, so let's clear them
            if(cfg == 0x00)
                *p_word = *p_word &~7;      //  9bit resolution, max conversion time = 93.75ms
            else
            if(cfg == 0x20)
                *p_word = *p_word &~3;      // 10bit resolution, max conversion time = 187.5ms
            else
            if(cfg == 0x40)
                *p_word = *p_word &~1;      // 11bit resolution, max conversion time = 375ms

            // Convert the raw bytes to a 16bit signed fixed point value :
            // 1 sign bit, 7 integer bits, 8 fractional bits (two's compliment
            // and the LSB of the 16bit binary number represents 1/256th of a unit).
            *p_word = *p_word << 4;
            // Convert to floating point value
            temp = toFloat(*p_word);

            __WARNING("non s - read with no errors\n");

            return 0;   // return with no errors
        }
    }

    __WARNING("sensor not present\n");

    return 1;   // error, sensor is not present
}

float DS1820::toFloat(uint16_t word) {
    if(word & 0x8000)
        return (-float(uint16_t(~word + 1)) / 256.0f);
    else
        return (float(word) / 256.0f);
}


```


    
  
