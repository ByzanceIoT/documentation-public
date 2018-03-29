# HC-SR04 Senzor

Tento program slouží na měření vzdálenost pomocí ultrazvukového modulu HC-SR04. Jedná se o kompaktní modul o velikosti velikosti cca 44x20mm, který je již samostatně funkční a není již potřeba připojovat další součástky.

## Hardware
* IDOA
* HC-SR04
* piezo
* LED
* nepájivé kontaktní pole

## Obvod

### Zapojení konektorů Senzoru:
1. 5V Supply 
2. Trigger Pulse Input
3. Echo Pulse Output
4. GND. 

Trigger: spouštěcí signál impuls TTL(5V) >10us 

Echo: výstupní signál TTL(5V) -> vzdálenost[cm] = doba_Echo[us] / 58


![](/assets/obrázek 14.png)  
## Code

Na začátu programu je potřeba definovat všechny pořebné proměnné a piny na které je připojený hardware. 

```#define```vytvoření vlastního makra. Jejich užívání je velice rozšířené, například je lze použít pro definování počtu prvků pole. Takové makro se pak používá v celém zdrojovém kódu a při změně počtu prvků pole stačí změnit jen makro. Makro se definuje za direktivou #define a lze jej zrušit direktivou #undef.

Po vyslání impulsu do modulu program počká na zpětné odeslání pulzu od modulu, kdy funkce Timer s názvem sonar nám vrátí potřebný počet mikrosekund. S tímto číslem můžeme dále pracovat. Vezmeme v úvahu rychlost zvuku 346,3 m*s-1 a to při teplotě suchého vzduchu 25°C. To znamená, že za 1mikrosekundu urazí v metrech 346,3/1000000 což je 0,0003463 metru. Převedo na cm to je 0,03463cm/mikrosekundu. Vzhledem k tomu, že signál jde od čidla k předmětu, kde se odrazí a zase zpět, musíme tuto vzdálenost ještě vydělit číslem 2. Výsledek je takový že se vzdálenost bude rovnat počtem mikrosekund násobených číslem 0,017315. Výsledek zašleme na seriový port a uložíme ho do proměnné distance.
Poté co program načte vzdálenost předmětu projde podmínky pomoci kterých rozbliká LED či rozhouká piezo pro upozornění na zapomenutý předmět(hrníček s kafem).


```cpp
#include "byzance.h"
#define cas 10
#define min 20
#define max 30
Serial pc(SERIAL_TX, SERIAL_RX);
DigitalOut trigger(X02);
DigitalIn  echo(X03);
PwmOut pwm(X15);
PwmOut led(X01);
Timer timer;
Timer casovac;
Timer sonar;
int correction = 0;
int i;

void blinkled(){
led.period(0.5f);
led.write(0.5f);
}
void bzucak(){
        pwm.period(0.10f);
        pwm.write(0.5f);
        Thread::wait(100);
        pwm.write(0.0f);
        wait(0);
}
void init(){
  pc.baud(115200);

}
void loop(){
  float distance = 0;
  float i=0;
  sonar.reset();
      sonar.start();
      while (echo==2) {};
      sonar.stop();
          trigger = 1;
          sonar.reset();
          wait_us(10.0);
          trigger = 0;
          while (echo==0) {};
          sonar.start();
          while (echo==1) {};
          sonar.stop();
          distance = (sonar.read_us())*0,017315;

          if(distance>min&&distance<max&&timer==0){
            pc.printf("dela se kava\n");
            Thread::wait(2000);
            timer.start();
          }
          if(distance<min||distance>max){
            timer.stop();
            timer.reset();

          }
          if(timer>cas){
            timer.stop();
            timer.reset();
            pc.printf("porad tu je\n");
            casovac.start();
            i=1;
            }
          if(distance>min&&distance<max&&i==1){
            blinkled();
            bzucak();
          }
          if(distance<min||distance>max||casovac.read()>30){
            led.write(0.0f);
            pwm=0;
            i=0;
            casovac.stop();
            casovac.reset();
          }
          
         pc.printf("%f",distance);
         pc.printf("\n");
         wait(0.2);
  }

```

