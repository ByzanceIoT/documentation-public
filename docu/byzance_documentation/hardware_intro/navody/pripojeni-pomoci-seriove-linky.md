# Připojení k PC pomocí sériové linky

Zařízení se dá k počítači připojit buď pomocí sériové linky s použitím FTDI převodníku, nebo se tato linka dá \[\[tutorial:usb\|softwarově emulovat přes USB\]\]. Ze strany počítače je tento přístup stejný a postup je jednotný.

# Windows

Každé sériové zařízení se standardně přihlašuje jako nový COM port. Seznam těchto portů je možné získat ve správci zařízení. To je možné zavolat například zkratkou ''WIN+X'' -&gt; ''Device Manager''. Je-li zařízeních víc, číslo konkrétního se dá zjistit například tak, že se zařízení několikrát fyzicky připojí a odpojí a přitom se jeho číslo objeví v seznamu a zase zmizí.



//obrázek

Neobjeví-li se zařízení, možná je třeba nainstalovat jeho ovladač. Windows 7 a Windows 10 by toto měly udělat automaticky. Dále je třeba mít nainstalovaný program Terminál. To může být například \[\[https://www.compuphase.com/software\_termite.htm\|Termite\]\], \[\[http://www.hw-group.com/products/hercules/index\_cz.html\|Hercules\]\] a mnoho jiných.



Zvolený COM port je třeba v nastavení terminálu společně s ukončovánímk řádků CR-LF, zvolenou rychlostí BAUD, data bits 8, stop bit 1, parita žádná. USB driver vyžaduje zapnutí flow control na RTS/CTS.



// obrázek



Po potvrzení nastavení je možné se zařízením začít komunikovat.



// obrázek

# MAC

Nové zařízení se v případě macOS přihlašuje přes porty s názvem "usbmodem" pro USB nebo "usbserial" pro sériovou linku. Pro snadné připojení je nejdříve vhodné nainstalovat utilitu {{:tutorial:coolterm.zip\|CoolTerm}}. V odkazovaném ZIP souboru je jak samotný program DMG a konfigurační soubor \*\*Yoda.stc\*\*.

Po nainstalování utility \*\*CoolTerm\*\* a spuštění konfiguračního souboru \*\*Yoda.stc\*\* je vhodné postupovat v následujících pěti krocích \(viz přiložený screenshot\):

* Stiskněte tlačítko Options v horním menu
* Re-Scanujte dostupné sériové porty
* Zvolte port "usbmodemXXXXX"/"usbserialXXXX" \(měl by být jediný\)
* Potvrďte stisknutím "OK"
* Stiskněte tlačítko "Connect" v horním menu

Nyní by se měl vypisovat log do okna aplikace.

V případě přepnutí na Bootloader v zařízení Yoda není nutné měnit port.

# Linux

Připojením zařízení k PC je v adresáři ''/dev/'' vytvořen soubor ''ttyUSBx'' nebo ''ttyACMx'', kde ''x'' je číslo. Výpis zařízení je tedy možné zobrazit pomocí správce souborů nebo příkazu ''ls /dev/tty\*''.

Jako komunikační terminál lze použít například cutecom či moserial. 

// obrázek

Na některých distribucích je nutné přidat uživatele do skupiny dialout pro přístup k sériovému portu. To je možné učinit příkazem

''sudo adduser už\_jméno dialout''.

# Ukázkový kód

Jednoduchý kód pro výpis ''hello word'' přes sériovou linku.

```cpp
#include "byzance.h"

Serial	pc(SERIAL_TX, SERIAL_RX);

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



