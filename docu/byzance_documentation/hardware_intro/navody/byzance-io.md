# Byzance IO

Blocko je online vizuální programovací nástroj, díky němuž je možné propojit s hardwarem a ovládat jednotlivé vstupy a výstupy. Sdružuje hardware, vstupy a výstupy z mobilní aplikace a logické bloky.

![](/assets/blocko.png)

Pro propojení hardware s blockem je nutné v hardware do kódu přidat speciálně definované vstupy, výstupy a případně zprávy. Ty je možné psát kdekoliv do souboru main.cpp.

Existuje 6 typů takovýchto definicí

```cpp
// digitalni vstup s nazvem din_name
DIGITAL_INPUT(din_name, {
    my_din_variable = value;
})

// analogovy vstup s nazvem ain_name
ANALOG_INPUT(ain_name, {
    my_ain_variable = value;
})

// message vstup s nazvem min_name a jednim parametrem typu STRING, volitelne jsou dalsi parametry
MESSAGE_INPUT(min_name, STRING, ... {
    pc.printf("message_in=%s, ...\n", arg1, ...);
});

// digitalni výstup s nazvem dout_name
DIGITAL_OUTPUT(dout_name);

// analogovy výstup s nazvem aout_name
ANALOG_OUTPUT(aout_name);

// message výstup s nazvem mout_name a jednim parametrem typu STRING, volitelne jsou dalsi parametry
MESSAGE_OUTPUT(mout_name, STRING, ...);
```

# Příklad použití

Kód pro rozsvícení LED na dálku může potom vypadat například takto

```cpp
#include "byzance.h"

DigitalOut MyLed(X00);

// digitalni vstup z blocka, ktery prebira hodnotu z blocka a primo rozsvicuje LED
DIGITAL_INPUT(blocko_led, {
    MyLed = value;
})

void init(){
    // neni treba nic inicializovat
}

void loop(){
    // neni treba nic delat
    Thread::wait(500);
}
```

# Omezení

Byzance vstupy a výstupy je momentálně možné implementovat pouze do souboru ''main.cpp'', jinak budou ignorovány.

