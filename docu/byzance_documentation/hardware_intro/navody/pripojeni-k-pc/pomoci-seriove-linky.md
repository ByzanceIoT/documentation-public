# Připojení k PC pomocí sériové linky



# Ukázkový kód

Jednoduchý kód pro výpis ''hello word'' přes sériovou linku.

```cpp
#include "byzance.h"

Serial    pc(SERIAL_TX, SERIAL_RX);

void init(){
   pc.baud(115200);
}

void loop(){
   pc.printf("hello world\n");
   Thread::wait(500);
}
```

Kód pro výpis ''hello world'' pomocí USB

```cpp
#include "byzance.h"

USBSerial usb;

void loop(){
   usb.printf("hello world\n");
   Thread::wait(500);
}
```



