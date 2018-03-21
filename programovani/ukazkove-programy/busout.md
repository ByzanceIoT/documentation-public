# BusOut
Tento program mění barvu RGB LED diody pomocí funkce ```BusOut```.
Barevný model RGB neboli červená-zelená-modrá je aditivní způsob míchání barev používaný v barevných monitorech a projektorech.


## Hardware 
* IODA
* 3x100Ω rezistor
* RGB LED
* nepájivé kontaktní pole

## Obvod
![](/assets/BusOut.png)

## Schéma
![](/assets/BusOut_schema.png)
## Code
Ve funkci ```void loop ()``` se mění napětí na pinech(Y01-Y03) a tím i barva RGB LED .

```cpp

   /** BusOut 
     * in this example we shows how to change coulour of RGB LED.
     */

#include "byzance.h"   // Include libraries for IODA.
BusOut myleds(Y01,Y02,Y03);   //The BusOut interface is used to create a number of DigitalOut pins that can be written as one value.
Serial pc(SERIAL_TX, SERIAL_RX);   // Defines the comunication interface if the serial line , SPI, CAN is needen in the program.

void init(){
  pc.baud(115200);   // Set baud rate.
}
void loop(){
   // iterate over the pins:
   for(int i=0; i<16; i++) {
      myleds = i;
      Thread::wait(0.25);
   }
}


```


