# Připojení pomocí USB

Některá Byzance zařízení je možné připojit pomocí USB. USB je koncipováno především k tomu, aby nahradilo standardní sériovou linku, čímž odpadne nutnost použití převodníku s FTDI čipem. Všeobecné informace, jak zprovoznit komunikaci ze strany počítače jsou popsány v článku [Připojení k PC](/byzance_documentation/hardware_intro/navody/pripojeni-k-pc.md).

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



