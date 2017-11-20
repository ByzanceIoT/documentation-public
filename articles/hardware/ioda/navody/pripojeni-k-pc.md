# Připojení zařízení k PC

Zařízení se dá k počítači připojit buď pomocí [sériové linky](/byzance_documentation/hardware_intro/navody/pripojeni-k-pc/pomoci-seriove-linky.md) s použitím FTDI převodníku, nebo se tato linka dá [softwarově emulovat přes USB](/byzance_documentation/hardware_intro/navody/pripojeni-k-pc/pomoci-usb.md). Ze strany počítače je tento přístup stejný a postup je jednotný.

## Windows

Každé sériové zařízení se standardně přihlašuje jako nový COM port. Seznam těchto portů je možné získat ve správci zařízení. To je možné zavolat například zkratkou ''WIN+X'' -&gt; ''Device Manager''. Je-li zařízeních víc, číslo konkrétního se dá zjistit například tak, že se zařízení několikrát fyzicky připojí a odpojí a přitom se jeho číslo objeví v seznamu a zase zmizí.

![](/images/com_port.png)

Neobjeví-li se zařízení, možná je třeba nainstalovat jeho ovladač. Windows 7 a Windows 10 by toto měly udělat automaticky. Dále je třeba mít nainstalovaný terminálový program. To může být například [Termite](https://www.compuphase.com/software_termite.htm), [Hercules](http://www.hw-group.com/products/hercules/index_cz.html) a mnoho jiných.

Zvolený COM port je třeba v nastavení terminálu společně s ukončovánímk řádků CR-LF, zvolenou rychlostí BAUD, data bits 8, stop bit 1, parita žádná. USB driver vyžaduje zapnutí flow control na RTS/CTS.

![](/images/termite.png)

Po potvrzení nastavení je možné se zařízením začít komunikovat.

![](/images/hello_world.png)

## MAC

Nové zařízení se v případě macOS přihlašuje přes porty s názvem "usbmodem" pro USB nebo "usbserial" pro sériovou linku. Pro snadné připojení je nejdříve vhodné nainstalovat utilitu // utilita coolterm. V odkazovaném ZIP souboru je jak samotný program DMG a konfigurační soubor \*\*Yoda.stc\*\*.

Po nainstalování utility \*\*CoolTerm\*\* a spuštění konfiguračního souboru \*\*Yoda.stc\*\* je vhodné postupovat v následujících pěti krocích \(viz přiložený screenshot\):

* Stiskněte tlačítko Options v horním menu
* Re-Scanujte dostupné sériové porty
* Zvolte port "usbmodemXXXXX"/"usbserialXXXX" \(měl by být jediný\)
* Potvrďte stisknutím "OK"
* Stiskněte tlačítko "Connect" v horním menu

![mac_connection](/images/mac_connection.png)

Nyní by se měl vypisovat log do okna aplikace.

V případě přepnutí na Bootloader v zařízení Yoda není nutné měnit port.

## Linux

Připojením zařízení k PC je v adresáři ''/dev/'' vytvořen soubor ''ttyUSBx'' nebo ''ttyACMx'', kde ''x'' je číslo. Výpis zařízení je tedy možné zobrazit pomocí správce souborů nebo příkazu ''ls /dev/tty\*''.

Jako komunikační terminál lze použít například cutecom či moserial.

![monserial](/images/moserial.png)

Na některých distribucích je nutné přidat uživatele do skupiny dialout pro přístup k sériovému portu. To je možné učinit příkazem

''sudo adduser už\_jméno dialout''.

# Programování sériové linky

Konkrétní ukázky kódu pro komunikaci s počítačem je možné nalézt v sekcích [komunikace pomocí USB](/byzance_documentation/hardware_intro/navody/pripojeni-k-pc/pomoci-usb.md) či [komunikace pomocí sériové linky](/byzance_documentation/hardware_intro/navody/pripojeni-k-pc/pomoci-seriove-linky.md).



# Připojení k PC pomocí USB

Některá Byzance zařízení je možné připojit pomocí USB. USB je koncipováno především k tomu, aby nahradilo standardní sériovou linku, čímž odpadne nutnost použití převodníku s FTDI čipem. Všeobecné informace, jak zprovoznit komunikaci ze strany počítače jsou popsány v článku [Připojení k PC](/byzance_documentation/hardware_intro/navody/pripojeni-k-pc.md). Nevýhoda je taková, že při každém restartu zařízení se USB odpojí a připojí k počítači a je třeba v ovládací aplikaci znovu otevřít COM port.

# Inicializace

Konstruktor USB linky může zůstat bez parametrů. V takovém případě se dosadí defaultní hodnoty. Nevýhodou může být to, že poslední parametr ''connect\_blocking'' je dosazen za ''true'', což znamená, že zařízení nepokračuje ve vykonávání kódu, dokud není připojeno USB a konstruktor je blokující. To může být v mnoha případech nežádoucí.

```cpp
USBSerial usb;
```

Vhodnější může být volba, aby USB konstruktor neblokoval kód, přičemž produktové kódy se musí dosadit do předchozích parametrů.

```cpp
USBSerial usb(0x1f00, 0x2012, 0x0001, false);
```

V případě USB se narozdíl od sériové linky nenastavuje baudová rychlost.

# Ukázkový kód

Velmi jednoduchý kód pro výpis ''hello world'' pomocí USB může vypadat například takto

```cpp
USBSerial usb;

void loop(){
   usb.printf("hello world\n");
   Thread::wait(500);
}
```

# Připojení k PC pomocí sériové linky

Sériová linka je poměrně standardní rozhraní využívané v oblasti mikrokontrolérů. Pro připojení se využívá [MBED-OS API](/byzance_documentation/hardware_intro/API/mbed-api.md) pro [komunikační rozhraní](/byzance_documentation/hardware_intro/API/mbed-api/komunikacni-rozhrani.md). Pro správnou funkčnost je třeba sériovou komunikaci [zprovoznit ze strany počítače](/byzance_documentation/hardware_intro/navody/pripojeni-k-pc.md).

## Inicializace

Většina zařízení je vybavena více sériovými linkami, což je třeba specifikovat při inicializaci. Je nutné zjistit konkrétní piny, které disponují touto periferií. Tyto informace se dají zjistit v sekci [Hardware](/Hardware) vždy pro konkrétní zařízení.

V konstruktoru se zadávají parametry pinů TX a RX.

```cpp
Serial pc(SERIAL_TX, SERIAL_RX);
```

Dále je třeba zvolit baudovou rychlost. K tomu je vyhrazena sekce init\(\). Baudová rychlost může být různá, záleží na uživateli a pohybuje se většinou v rozmezí 1200 - 230400 baud. Stejnou rychlost je třeba nastavit [na straně počítače při připojení](/byzance_documentation/hardware_intro/navody/pripojeni-k-pc.md).

```cpp
pc.baud(115200);
```

## Ukázkový kód

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







