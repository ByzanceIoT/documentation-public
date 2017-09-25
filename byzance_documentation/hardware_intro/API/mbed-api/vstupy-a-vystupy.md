# Vstupy a výstupy

# AnalogIn

Převede napětí na pinu analogového vstupu v rozmezí 0 - 3.3V do digitální podoby a interpretujep ho číslem na škále 0-4095. Rozlišení převodníku je 2.44 mV. 

```cpp
AnalogIn ain(pin_name);
printf(”ain value = %3.3f%%\n”, ain.read());
```

## AnalogOut

Nastaví napětí na pinu analogového výstupu v rozmezí 0 - 3.3V zadáním hodnoty 0-4095. Každá jednotka interpretuje 2.44mV.

```cpp
AnalogOut aout(pin_name);
aout.write(some_float);
```

## DigitalIn

Přečte hodnotu digitálního vstupu

```cpp
DigitalIn din(pin_name);
printf("pin has value : %d \n", din.read());
```

## DigitalOut

Nastaví na digitálním vástupu logickou úroveň.

```cpp
DigitalOut dout(pin_name);
dout=1;
```

## DigitalInOut

Obousměrný digitální pin, kombinace digitálního vstupu a digitálního výstupu. 

```cpp
DigitalInOut diout(pin_name);

// configure as output
diout.output();

// set HIGH
diout = 1;

// configure as input
diout.input();

// read value of pin
pc.printf("diout value = %d \n", diout.read());
```

## BusIn

Umožňuje definovat seznam digitálních pinů, jejichž hodnota lze přečíst jako jedno číslo. 

 
```cpp

// Tři přepínače vedené jako BUS připojené na vstupy X1,X2,X3
BusIn switches(X01,X02,X03);

void init(){

//Nastavení módu přepínačů (PullUp/PullDown/PullNone/OpenDrain)
switches.mode(PullNone);
}
void loop(){

  // Přečte digitální vstupy a    
  switch(switches.read()){
  // na základě hodnoty vypíše, která kombinace přepínačů je navolená.
  
      case 0x0: printf("everything LOW\n"); break;
      case 0x1: printf("X01-UP X02-DOWN X03-DOWN\n"); break;
      case 0x2: printf("X01-DOWN X02-UP X03-DOWN\n"); break;
      case 0x3: printf("X01-UP X02-UP X03-DOWN\n"); break;
      case 0x4: printf("X01-DOWN X02-DOWN X03-UP\n"); break;
      case 0x5: printf("X01-UP X02-DOWN X03-UP\n"); break;
      case 0x6: printf("X01-DOWN X02-UP X03-UP\n"); break;
      case 0x7: printf("X01-UP X02-UP X03-UP\n"); break;
  }


}
```

## BusOut

Definuje seznam digitálních výstupů, které lze přepsat jedním číslem. 

```cpp
//Tři Led diody připojené na digitální výstupy X01, X02, X03 
BusOut leds(X01, X02, X03); 

void loop(){

//Postupné zobrazení čísla 0-8 v binární podobě na LED
  for(int i = 0; i < 8, i++){
    leds = i; 
    wait(0.25);
  }

}
```

## BusInOut

Definuje bus, ze kterého je možné jak číst, tak do něj i zapisovat.

```cpp

BusInOut io_bus(X01, X02, X03);

void loop(){

  io_bus.output(); // Nastaví bus na BusOut
  io_bus = 5;
  wait(5);
  io_bus.input();  // Nastaví bus na BusIn
  wait(5);
  if(io_bus == 0x6){
    printf("NUMBER 6!\n");
  }
}
```

## PortIn

PortIn má stejnou funkci jako BusIn,je o dost rychlejší ale méně flexibilnější 

```cpp

// Argumentem konstruktoru je číslo portu a číslem určené piny tohoto portu
PortIn p2(port2, 0x0000003F); // pin 21 - 26  

void init(){
  //Nastavení módu portu
  p2.mode(PullNone); 
}
void loop(){
  int pins = p.read();
  if(pins){ //alespoň jeden vstup z portu má hodnotu jedna
    printf("At least one switch is turned on");
  }
}

```

## PortOut

Port Out nahrazuje BusOut, stejně jako PortIn je rychlejší ale méně flexibilnější

```cpp
#define LED_SHIELD 0x00B40000

PortOut port(Port2, LED_SHIELD);

void loop(){
  port=LED_MASK;
  wait(1);
  port=0;
  wait(1);

}
```

## PortInOut

Třída PortInOut kombinuje funkce PortIn a PortOut a mód této funkce lze nastavovat za běhu programu. 
 
```cpp
#define LED_SHIELD 0x00B40000
PortOut port(Port2, LED_SHIELD);

void loop(){
  port.input();
  int port_value = port;
  port.output();
  port=LED_MASK;
  wait(1);
  port=0;
  wait(1);

}

```

## PwmOut

Funkce PwmOut umožňuje na pinu vytvářet pulzně šířkovou modulaci, regulovat její periodu a šířku jejich pulsů.

```cpp

PwmOut pwm(X04);

void loop(){
    
  pwm.period(4.0f);  //Natavení periody 4s 
  pwm.write(0.50f);  //50% duty cycle, vzhledem k periodě
  
  wait(10);
  
  pwm.period(4.0f);   //nastavení periody 4s
  pwm.pulsewidth(2);  //dvouvteřinový puls -> stejné jako 50% duty cycle
  
  
}

```

## InterruptIn

Připojením interruptu na konkrétní pin, lze okamžitě reagovat akcí na změnu digitální hodnoty tohoto pinu.

```cpp
InterruptIn button(X08); //Připojení interruptu k pinu X08
DigitalOut led(X05);

void pushed_button(){ //Při stisknutí tlačítka změn logickou hodnotu na pinu X05
 led = !led;
}

void init(){

button.rise(&pushed_button); //Připojení adresy funkce pushed_button na náběžnou hranu pinu X08 

}

```



