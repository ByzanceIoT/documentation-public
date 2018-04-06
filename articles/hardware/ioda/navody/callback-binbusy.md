# Callback Busy

Tento callback je funkcí knihovny Byzance, která slouží k oznamování, že zařízení je ve stavu **busy**. Stav **busy** indikuje, že zařízení provádí update nového firmware, nebo přípravu na tento update. V tomto stavu v pozadí probíhá procesorově náročnější operace, která ovšem může být přerušována aktuálně probíhajícím uživatelským programem. Callback Busy slouží k ošetření uživatelského programu, aby neblokoval procesy probíhající v pozadí a k přípravě zařízení na restart, který je proveden po updatu nového firmware. K zavolání callbacku může dojít v průběhu vykonávání programu i několikrát po sobě - typicky při přípravě na update a posléze při aktualizaci samotné. Po dokončení update uživatelského programu může dojít k restartu zařízení.

Uživatelská funkce \(callback\), která má být provedena v případě přepnutí do stavu "busy", se připojí pomocí následující konstrukce

```cpp
Byzance::attach_bin_busy(&<user-function-name>);
```

Využití callbacku Busy je vhodné v případě, kdy je v programu často voláno přerušení\(ISR\), které by mohlo potřebovat většinu procesorového času na pozadí. Takovým případem může být například velmi často volaný Ticker. Dále je vhodné callback využít v případě, kdy je nutné ošetřit chování zařízení a ostatních připojených systémů v případě aktualizace. Takovým případem může být libovolný aktuátor, který by se v nejhorším případě mohl v průběhu update stát neovladatelným.

Uživatelská funkce připojená ke callbacku je volána pokaždé, když se změní stav busy a tato informace je zároveň předána v argumentu volané funkce

```cpp
// Function attached to busy callback - called when the busy state change
void busy_function(bool busy){

    if(busy){

      // Disable interrupts  
      // Detach tickers 
      // Turn off actuators (Motors, pumps, )
      // etc ..  

    } else {

      // Enable interrupts
      // Attach tickers again 
      // etc ..     

    }

}
```

## Ukázka kódu

Následující ukázka kódu při startu programu inicializuje ticker, který může vykonávat nějakou činnost.

```cpp
Ticker tic;
Serial pc(SERIAL_TX, SERIAL_RX);


void ticker_fnc(){

    // DO SOMETHING USEFUL

}

// Function called when the device is in busy state 
void bin_busy(bool busy){
    if(busy){

        // detach
        pc.printf("*** BUSY: detaching ticker\n");
        tic::attach(NULL);

        // Disable other interrupts 
        // Turn motors off before restart 
        // Turn off other actuators 
        // etc .. 

    }
}

void init() {

    // Attach ticker function 
    tic.attach(&ticker_fnc);

    // Attach function "bin_busy" to Busy callback
    Byzance::attach_bin_busy(&bin_busy);    

}
```



