#Callback Busy

Tento callback je funkcí knihovny Byzance, která slouží ke zpětné informaci o tom, že zařízení je ve stavu **busy**. Stav **busy** indikuje, že zařízení provádí update nového firmware, nebo zálohu aktuálního firmware v rámci funcke [Autobackup](/articles/hardware/ioda/navody/autobackup.md). V tomto stavu v pozadí probíhá časově náročnější datový přenos, který ovšem může být přerušen aktuálně probíhajícím uživatelským programem. Callback Busy slouží k ošetření uživatelského programu, aby nepřerušoval procesy probíhající v pozadí a k přípravě zařízení na restart který je proveden po updatu nového firmware. 

Uživatlskou funkci, které má být provedena v případě změny stavu busy lze provést voláním příkazu


```
Byzance::attach_bin_busy(&<user-function-name>);
```

Využití callbacku Busy je vhodné v případě, kdy je v programu často voláno přerušení(ISR), které by mohlo odebrat většinu 
procesorového času procesům v pozadí. Takovým případem může být například velmi často volaný Ticker. Dále je vhodné callback využít v případě, kdy je nutné ošetřit chování zařízení a ostatních připojených systémů v případě restartu. Takovým případem může být libovolný aktuátor, který se automaticky nevypne při restartu IODY a mohl by se stát neovladatelným.

Uživatelská funkce připojená ke callbacku je volána pokaždé když se změní stav busy a tento stav je zároveň předán v argumentu volané funkce 


```
// Function attached to busy callback - called when the busy state change
void busy_function(bool busy){

    if(busy){
    
      // Disable interrupts  
      // Detach tickers 
      // Turn off actuators (Motors, pumps, )
      // etc ..  
      
    }else{
    
      // Enable interrupts
      // Attach tickers again 
      // etc ..     
    
    }

}

```



## Ukázka kódu

```

Ticker tic;
Serial pc(SERIAL_TX, SERIAL_RX).


// Function called when the device is in busy state 
void bin_busy(bool busy){
    if(busy){
    
        to_computer("*** BUSY: detaching ticker\n");
        Display_controler::detach_ticker();
        
        // Disble other interrupts 
        // Turn motors off before restart 
        // Turn off other actuators 
        // etc .. 
    
    }
}

void init() {

    // Attach function "bin_busy" to Busy callback
    
    Byzance::attach_bin_busy(&bin_busy);    

}

```


