# Časování

## [Ticker](https://os.mbed.com/docs/latest/reference/ticker.html)

Umožňuje periodické volání funkcí s mikrosekundovou přesností.

Příklad demonstruje využití tickeru pro účely blikání LED diodou. Každé 2 sekundy je invertován stav modré LED. Tímto je dosaženo blikání z kontextu ISR.

```cpp
#include "byzance.h"

Serial pc(SERIAL_TX, SERIAL_RX);	//USBSerial pc(0x1f00, 0x2012, 0x0001, false); //
Ticker ticker;
DigitalOut led(LED_BLUE);
​
void flip() {    
    led = !led;    //blue led is blinking
}
​
void init(){
    Byzance::led_module(false);  //disable LED module for Byzance
    ticker.attach(&flip,2.0);    //call funciton flip every 2 seconds
}
​
void loop(){
    pc.printf("im running\n");
    Thread::wait(1000);
}
```

## [Timeout](https://os.mbed.com/docs/latest/reference/timeout.html)

Umožňuje zpožděné volání příslušné funkce s mikrosekundovou přesností.

Příklad demonstruje využití třídy Timeout pro zpožděné vypnutí modré LED diody. Dioda je vypnuta po 2 sekundách.

```cpp
#include "byzance.h"

Serial pc(SERIAL_TX, SERIAL_RX);	//USBSerial pc(0x1f00, 0x2012, 0x0001, false); //
Timeout timeout;
DigitalOut led(LED_BLUE);    //led control is inverted

void turn_off() {    
    led = 1;    //turn off blue led
}

void init(){
    Byzance::led_module(false);      //disable LED module for Byzance
    led = 0;                         //turn on blue led
    timeout.attach(&turn_off,2.0);    //call funciton turn_off after 2 seconds
}

void loop(){
    pc.printf("im running\n");
    Thread::wait(1000);
}
```

## [Timer](https://os.mbed.com/docs/latest/reference/timer.html)

Umožňuje měření časových úseků až s mikrosekundovou přesností. 

Příklad demonstruje využití časovače - pokud měřený časový úsek přesáhne 2 sekundy, je invertována modrá LED dioda a časovač vynulován a znovu spuštěn. Tímto je dosaženo blikání z kontextu vlákna.

```cpp
#include "byzance.h"

Serial pc(SERIAL_TX, SERIAL_RX);	//USBSerial pc(0x1f00, 0x2012, 0x0001, false); //
DigitalOut led(LED_BLUE);
Timer timer;

void init(){
    Byzance::led_module(false);      //disable LED module for Byzance
    timer.start();                   //start the timer
}

void loop(){
    if(timer.read_ms() > 2000){    //if timer exceedes 2000ms
        timer.stop();    //stop the timer
        timer.reset();   //reset the timer to zero
        led = !led;      //flip the LED
        timer.start();   //and start timer again
    }
    Thread::wait(50);
}
```



