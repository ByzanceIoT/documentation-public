# Práce s datem a časem \(RTC\)

Každé Byzance zařízení je vybaveno obvodem pro udržování reálného času \(RTC\). Jeho obsluha je poměrně triviální a dodržuje [standardy C++](http://www.cplusplus.com/reference/ctime/time/).

Čas je synchronizován automaticky při připojení k Homerovi. Toto je možné vypnout v [bootloaderu](/byzance_documentation/hardware_intro/features/bootloader.md).

Základní jednotkou je Unixové časové razítko, které reprezentuje počet sekund, které uplynuly od 1.1. 1970. K převodu jednotek je možné využít například jeden z mnoha [online nástrojů](http://www.onlineconversion.com/unix_time.htm).

## Ukázka pro práci s Unix timestamp

```cpp
#include "byzance.h"

// serial line init
Serial pc(SERIAL_TX, SERIAL_RX);

// time object
time_t timestamp;

void init(){

    pc.baud(115200\);
    pc.printf("RTC test\n");

    // unix timestamp setter
    timestamp = 1234567890;    
    set_time(timestamp);    
    pc.printf("Time set\n");
}

void loop(){

    // unix timestamp getter
    time(&timestamp);    
    pc.printf("Timestamp is %u\n",(unsigned int) timestamp);    
    Thread::wait(1000);
}
```

# Vlastní časové pásmo a parsování timestamp do struktury

Časové razítko je v zařízení automaticky nastaveno nastaveno na UTC pásmo. Pro vlastní offset od UTC je třeba příslušnou položku změnit v [command režimu bootloaderu](/byzance_documentation/hardware_intro/features/bootloader/command-rezim.md). Nastavený offset se za běhu normálního programu získat pomocí veřejné funkce ''Byzance::get\_timeoffset\(\)''.

S tím souvisí i parsování podle regionálního nastavení. K unixovému časovému razítku se přičte lokální offset a výslednou položku je možné konvertovat do časové struktury funkcí [gmtime\(\)](http://www.cplusplus.com/reference/ctime/gmtime/).

```cpp
#include "byzance.h"

Serial    pc(SERIAL_TX, SERIAL_RX); // tx, rx

void init(){

    pc.baud\(115200\);
    pc.printf\("Time demo\n"\);

    time_t time_utc;
    time_t time_local;

    struct tm *p_utc;
    struct tm *p_local;

    p_utc    = (tm*)malloc(sizeof(tm));
    p_local  = (tm*)malloc(sizeof(tm));

    // load UTC time to variable    
    time(&time_utc);

    // calculate local time using timeoffset getter    
    time_local = time_utc + Byzance::get_timeoffset();

    // convert UTC from timestamp to time struct    
    memcpy(p_utc, gmtime(&time_utc), sizeof(tm));    
    pc.printf("UTC time   = %2d:%02d\n", (p_utc  -&gt;tm\_hour\)%24, p_utc  -&gt;tm_min);

    // convert localtime from timestamp to time struct    
    memcpy(p_local, gmtime(&time_local), sizeof(tm));    
    pc.printf("Local time = %2d:%02d\n", (p_local-&gt;tm_hour)%24, p_local-&gt;tm_min\);
}
```



