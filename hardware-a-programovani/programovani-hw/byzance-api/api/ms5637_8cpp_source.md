---
search: false
---

# ms5637.cpp File Reference

**[Go to the documentation of this file.](ms5637_8cpp.md)**
Source: `D:/w/hw-libs/\_libs\_/libraries/ms5637.cpp`

    
    
    
    
      
      
    
    
    
```cpp
/*
 * ms5637.cpp
 *
 *  Created on: 9. 8. 2017
 *      Author: martin
 */

#include "mbed.h"
#include "ms5637.h"

REGISTER_DEBUG(MS5637);

double P;                       // compensated pressure value (mB)
double T;                       // compensated temperature value (degC)
double A;                       // altitude (ft)
double S;                       // sea level barometer (mB)

unsigned int C[8];                  //coefficient storage

//--------------------------------------------------------------------------------------------------------------------------------------//
// Constructor and destructor

ms5637::ms5637(I2C *i2c):  _i2c(i2c) {
        _sensor_present = false;
}


//********************************************************
//********************************************************

int8_t ms5637::m_i2c_send(char cmd, bool repeated) {

    int8_t ret = _i2c->write(MS5637_ADDR, &cmd, 1, repeated);
    if(ret){
        __ERROR("ms5637: i2c write error: %d\n", ret);
    }
    return ret;
    /*
    unsigned char ret;
    ret = m_i2c_start(false);
    if(!(ret)) {
        m_i2c_stop();
    } else {
        ret = m_i2c_write(cmd);
        m_i2c_stop();
    }*/
}

//********************************************************
//********************************************************

int8_t ms5637::cmd_reset() {

    int8_t ret = 0;

    __TRACE("sending reset\n");
    int i = 0;
    do{
        ret = m_i2c_send(MS5637_CMD_RESET);
        i++;
        if(ret){
            __ERROR("was not reset for %d time\n",i);
        }
    }while(ret != 0 && i<5);

    if(ret){
        __ERROR("reset error\n");
        _sensor_present = false;
        return -2;
    }
    __TRACE("reset sent\n");

    wait_ms(4);

    __TRACE("loading coefs\n");
    ret = loadCoefs();
    if(ret){
        __ERROR("crc error while reading coefs\n");
        _sensor_present = false;
        return -3;
    }
    __TRACE("coefs loaded\n");

    if(ret!=0){
        _sensor_present=false;
        return -1;
    }else{
        _sensor_present=true;
        return 0;
    }
}

//********************************************************
//********************************************************

int32_t ms5637::cmd_adc(char cmd) {

    char cobuf[3];
    cobuf[0] = 0;
    cobuf[1] = 0;
    cobuf[2] = 0;
    unsigned int ret;
    unsigned long temp = 0;

    __TRACE("start, cmd = %d\n", cmd);

    // initiate pressure conversion
    ret = m_i2c_send(MS5637_CMD_ADC_CONV + cmd);
    if(ret){
        __ERROR("ms5637: i2c error: %d\n", ret);
        return -1;
    }

    switch (cmd & 0x0f) {
        case MS5637_CMD_ADC_256 :
            // datasheet says 500us
            wait_us(900);
            break;
        case MS5637_CMD_ADC_512 :
            // datasheet says 1.1ms
            wait_ms(3);
            break;
        case MS5637_CMD_ADC_1024:
            // datasheet says 2.1ms
            wait_ms(4);
            break;
        case MS5637_CMD_ADC_2048:
            // datasheet says 4.1ms
            wait_ms(6);
            break;
        case MS5637_CMD_ADC_4096:
            // datasheet says 8.22ms
            wait_ms(10);
            break;
    }

    // ADC read sequence
    ret = m_i2c_send(MS5637_CMD_ADC_READ);
    if(ret){
        __ERROR("ms5637: i2c error: %d\n", ret);
        return -1;
    }

    //I2C answer from ms5637
    // dont send stop at end
    ret = _i2c->read(MS5637_ADDR_R, cobuf, 3);
    if(ret){
        __ERROR("ms5637: i2c error: %d\n", ret);
        return -1;
    }

    temp = (cobuf[0] << 16) + (cobuf[1] << 8) + cobuf[2];

    __TRACE("end, temp = %d\n", temp);

    return temp;
}

//********************************************************
//********************************************************

unsigned int ms5637::cmd_prom(char coef_num) {
    char cobuf[2];
    unsigned int ret;
    unsigned int rC = 0;
    cobuf[0] = 0;
    cobuf[1] = 0;

    // send PROM READ command
    ret = m_i2c_send(MS5637_CMD_PROM_RD + coef_num * 2);
    if(ret){
        __ERROR("prom cmd error = %d\n", ret);
        return 0;
    }

    // I2C answer from ms5637
    // not ack at end
    ret = _i2c->read(MS5637_ADDR_R, cobuf, 2);
    if(ret){
        __ERROR("prom read error = %d\n", ret);
        return 0;
    }

    rC = cobuf[0] * 256 + cobuf[1];

    __TRACE("coef num = %d, val = %u\n", coef_num, rC);

    return rC;
}

//********************************************************
//********************************************************
unsigned char ms5637::crc4(unsigned int n_prom[]) {

    int cnt; // simple counter
    unsigned int n_rem=0; // crc reminder
    unsigned char n_bit;

    n_prom[0]=((n_prom[0]) & 0x0FFF); // CRC byte is replaced by 0
    n_prom[7]=0; // Subsidiary value, set to 0

    // operation is performed on bytes
    for (cnt = 0; cnt < 16; cnt++) { // choose LSB or MSB
        if (cnt%2==1){
            n_rem ^= (unsigned short) ((n_prom[cnt>>1]) & 0x00FF);
        } else {
            n_rem ^= (unsigned short) (n_prom[cnt>>1]>>8);
        }

        for (n_bit = 8; n_bit > 0; n_bit--) {
            if (n_rem & (0x8000)){
                n_rem = (n_rem << 1) ^ 0x3000;
            } else {
                n_rem = (n_rem << 1);
            }
        }
    }

    n_rem= ((n_rem >> 12) & 0x000F); // final 4-bit reminder is CRC code

    return (n_rem ^ 0x00);
}

//********************************************************
//********************************************************

bool ms5637::loadCoefs() {

    unsigned int crc_stored     = 0x00;
    unsigned int crc_calculated = 0x00;

    __TRACE("loading coefs\n");

    for (int i = 0; i < 7; i++){
        C[i] = cmd_prom(i);
        __TRACE("C[i] = %d\n", i, C[i]);
    }

    __TRACE("loading done\n");

    // determine stored crc
    crc_stored      = C[0]>>12;

    // this function clears CRC in C and sets subsidiary 7th bit to 0
    crc_calculated  = crc4(C);

    if(crc_stored != crc_calculated){

        __ERROR("crc error (calculated = %d, stored = %d\n", crc_calculated, crc_stored);

        return true;
    }

    // CRC ok
    return false;

}

//********************************************************
//********************************************************

void ms5637::calcPT() {

    int32_t D1 = cmd_adc(MS5637_CMD_ADC_D1 + MS5637_CMD_ADC_4096); // read D1
    if(D1 < 0){
        __ERROR("ms5637: could not get D1: %d\n", D1);
        return;
    }

    int32_t D2 = cmd_adc(MS5637_CMD_ADC_D2 + MS5637_CMD_ADC_4096); // read D2
    if(D2 < 0){
        __ERROR("ms5637: could not get D2: %d\n", D2);
        return;
    }

    double dT = D2 - C[5] * 256;
    double OFF_var  = C[2] * 131072.0 + (C[4] * dT) / 64.0;     //was  OFF  = (C[2] << 17) + dT * C[4] / (1 << 6);
    double SENS = C[1] * 65536 + (C[3] * dT) / 128.0;     //was  SENS = (C[1] << 16) + dT * C[3] / (1 << 7);

    //T = (2000 + (((uint64_t)dT * C[6]) / (float)(1 << 23))) / 100;
    T=(double)(2000+(dT*C[6])/8388608)/100;
    //int32_t TEMP = 2000 + (int64_t)dT * (int64_t)C[6] / (int64_t)(1 << 23);
    int32_t TEMP = 2000 + (int64_t)dT * (int64_t)(C[6] >> 23);
    if(TEMP < 2000) { // if temperature lower than 20 Celsius
        float T1 = (TEMP - 2000) * (TEMP - 2000);
        int64_t OFF1_var  = (61 * T1) / 16;
        int64_t SENS1 = (29 * T1) / 16;

        if(TEMP < -1500) { // if temperature lower than -15 Celsius
            T1 = (TEMP + 1500) * (TEMP + 1500);
            OFF1_var  += 17 * T1;
            SENS1 += 9 * T1 ;
        }
        OFF_var -= OFF1_var;
        SENS -= SENS1;
        T = (float)TEMP / 100;
    }
//    int64_t P1 = ((((int64_t)D1 * SENS) >> 21) - OFF) >> 15;
    //P = ((((int64_t)D1 * SENS ) >> 21) - OFF) / (double) (1 << 15) / 100.0;
    P=(((double)((double)D1*SENS)/2097152.0)-OFF_var)/32768.0;

    P/=100.0; // convert to hpa/mbar

    //__ERROR("P = %f\n", P);
}

//********************************************************
//********************************************************

double ms5637::calcTemp() {

    if(!_sensor_present){
        __ERROR("sensor is not present\n");
        return 0;
    }

    __TRACE("calculating PT\n");
    calcPT();
    __TRACE("PT calculated\n");

    return(T);
}

//********************************************************
//********************************************************

double ms5637::calcPressure() {

    if(!_sensor_present){
        __ERROR("sensor is not present\n");
        return 0;
    }

    __TRACE("calculating PT\n");
    calcPT();
    __TRACE("PT calculated\n");

    return(P);
}

//********************************************************
//********************************************************

double ms5637::getPressure() {

    if(!_sensor_present){
        __ERROR("sensor is not present\n");
        return 0;
    }

    __TRACE("calculating PT\n");
    calcPT();
    __TRACE("PT calculated\n");

    return(P);
}

//********************************************************
//********************************************************

float ms5637::getAltitudeFT(float sea_pressure) {
    if(!_sensor_present){
        __ERROR("sensor is not present\n");
        return 0;
    }
    A = (1 - (pow((P / (double)sea_pressure), 0.190284))) * 145366.45;
    return((float)A);
}

//********************************************************
//********************************************************

float ms5637::getSeaLevelBaroFT(float known_alt) {
    if(!_sensor_present){
        __ERROR("sensor is not present\n");
        return 0;
    }
    S = pow(pow((P * INHG), 0.190284) + 0.00001313 * known_alt , 5.2553026) * MB;
    return((float)S);
}

//********************************************************
//********************************************************

float ms5637::getSeaLevelBaroM(float known_alt) {
    if(!_sensor_present){
        __ERROR("sensor is not present\n");
        return 0;
    }
    S = pow(pow((P * INHG), 0.190284) + 0.00001313 * known_alt * FTMETERS , 5.2553026) * MB;
    return((float)S);
}



```


    
  
