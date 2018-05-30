---
search: false
---

# ms5637.h File Reference

**[Go to the documentation of this file.](ms5637_8h.md)**
Source: `D:/w/hw-libs/\_libs\_/libraries/ms5637.h`

    
    
    
    
    
    
    
    
      
    
    
    
```cpp
#ifndef LIBRARIES_MS5637_H_
#define LIBRARIES_MS5637_H_

#include "mbed.h"
#include "ByzanceLogger.h"
#include "byzance_debug.h"


#define SEA_PRESS   1013.25                 //default sea level pressure level in mb
#define KNOWNALT    327.0                   //default known altitude, 5200 Franklin Dr., 94588
#define INHG        0.02952998751           //convert mb to in/Hg constant
#define MB          33.8638815              //convert in/Hg to mb constant
#define FTMETERS    0.3048                  //convert feet to meters


//_____ M A C R O S
#define MS5637_ADDR 0xEC
#define MS5637_ADDR_W 0xEC // Module address write mode CHANGED FOR 5637 ORIGINAL 0Xee
#define MS5637_ADDR_R 0xED // Module address read modeCHANGED FOR 5637 ORIGINAL 0XeF
#define MS5637_CMD_RESET 0x1E // ADC reset command
#define MS5637_CMD_ADC_READ 0x00 // ADC read command
#define MS5637_CMD_ADC_CONV 0x40 // ADC conversion command
#define MS5637_CMD_ADC_D1 0x00 // ADC D1 conversion
#define MS5637_CMD_ADC_D2 0x10 // ADC D2 conversion
#define MS5637_CMD_ADC_256 0x00 // ADC OSR=256
#define MS5637_CMD_ADC_512 0x02 // ADC OSR=512
#define MS5637_CMD_ADC_1024 0x04 // ADC OSR=1024
#define MS5637_CMD_ADC_2048 0x06 // ADC OSR=2048
#define MS5637_CMD_ADC_4096 0x08 // ADC OSR=4096
#define MS5637_CMD_PROM_RD 0xA0 // Prom read command

class ms5637 {

public:
    ms5637(I2C *i2c);
    int8_t cmd_reset();
    double calcTemp();
    double calcPressure();
    double getPressure();
    float getAltitudeFT(float sea_pressure);
    float getSeaLevelBaroFT(float known_alt);
    float getSeaLevelBaroM(float known_alt);

private:
    bool _sensor_present;
    int8_t m_i2c_send(char cmd, bool repeated = false);
    bool loadCoefs();
    int32_t cmd_adc(char cmd);
    unsigned int cmd_prom(char coef_num);
    unsigned char crc4(unsigned  n_prom[]);
    void calcPT();
    unsigned int PTbuffer[8];       // calibration coefficients

protected:
    I2C     *_i2c;


};




#endif /* LIBRARIES_MS5637_H_ */
```


    
  
