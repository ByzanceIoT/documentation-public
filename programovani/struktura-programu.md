## Struktura programu

Základem při psaní zdrojového kódu je využití open-source operačního systému MBED-OS. Kód se píše především v online rozhraní Becki Byzance. TO DO - odkaz na článek o becki
V první části programu, nejlépe již na prvním řádku, je nutné importovat knihovnu Byzance pomocí příkazu:
#include "byzance.h"
Tato knihovna má za úkol automaticky inicializovat periferie, připojit desku k internetu a inicializovat vlákna, která se starají o update zdrojového kódu a připojení k serverům. Includem knihovny se zpřístupní Byzance API a uživatelská makra.
TO DO!!!! Následovat by měla definice vstupů a výstupů pro blocko, ale Code server si s tím poradí v celém main souboru.
Více viz Byzance IO.
//definice virtuálních vstupů a výstupů
V další části kódu se poté definují fyzické vstupy a výstupy desky viz MBED vstupy a výstupy
// Definice fyzických vstupů a výstupů
DigitalOut D1(X02);
DigitalIn D2(X05);
AnalogOut A1(Y23);
Poté je vhodné inicializovat globální proměnné a objekty jako například sériová komunikace atd.
Serial pc(SERIAL_TX_pin, SERIAL_RX_pin); // tx, rx
TO DO - přeformulovat následující odstavec Po inicializaci proměnných je možné implementovat funkci pre_init(). Tato funkce je spuštěna předtím, než je inicializováno vlákno Byzance a předtím než se zažízení připojí k serverům. Tuto funcki není nutné implementovat, nicméně je vhodná v případě debugu.
void pre_init(){

}
Následuje inicializační část, která je automaticky zavolána právě jednou po startu zařízení.
void init(){
    pc.printf("Hello world\n");
}
Poslední je část kódu, který se bude vykonávat ve smyčce. Slouží jako náhrada while(true) cyklu v klasické main funkci. Jediným rozdílem je to, že mezi každým loop() se automaticky dává prostor i Byzance vláknu a resetuje se watchdog.
void loop(){
    pc.printf("Test\n");
    Thread::wait(500);
}