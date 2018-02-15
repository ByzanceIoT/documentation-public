#Callback Busy

Tento callback je funkcí knihovny Byzance, která slouží ke zpětné informaci o tom, že zařízení je ve stavu **busy**. V tomto stavu se zařízení nachází pokud je prováděn nějaký časově náročnější proces jako například update nového firmware nebo jeho [záloha](/articles/hardware/ioda/navody/autobackup.md). Využití callbacku busy je vhodné v případě, kdy je v uživatelském programu velmi často voláno přerušení (například časté volání tickeru). Tím může by dojít k situaci, ve které procesy probíhající v pozadí nebudou mít k dispozici dostatek procesorového času (Nemusí se provést update nového firmware, nebo může trvat několikrát déle). 

Dále se tento callback využívá v případě, kdy chceme zamezit nepředvídatelnému chování, ke kterému může dojít při restartu zařízení po updatu nového firmware. 

Pomocí tohoto callbacku lze tedy ve stavu busy zavolat uživatelskou funkci, ve které lze omezit volání přerušení během updatu nebo zálohy firmware a zároveň připravit zařízení na blížící se restart.



```

// Function called when the device is in busy state 
void bin_busy(bool busy){
    if(busy){
    
        to_computer("*** BUSY: detaching ticker\n");
        Display_controler::detach_ticker();
        
        // Disble other interrupts 
        // Turn motors off
        // etc .. 
    
    }
}

void init() {

// Attach function "bin_busy" to Busy callback
Byzance::attach_bin_busy(&bin_busy);    

}

```


