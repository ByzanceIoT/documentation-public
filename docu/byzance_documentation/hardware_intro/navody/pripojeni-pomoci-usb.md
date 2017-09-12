# Připojení pomocí USB

Zařízení YODAG2 a YODAG3E je možné připojit pomocí USB. USB je koncipováno především k tomu, aby nahradilo standardní sériovou linku, čímž odpadne nutnost použití převodníku s FTDI čipem.

# Softwarová inicializace zařízení na straně YODA

Konstruktor USB linky může zůstat bez parametrů. V takovém případě se dosadí defaultní hodnoty. Nevýhodou je to, že poslední parametr ''connect\_blocking'' je dosazen za ''true'', což znamená, že zařízení nepokračuje ve vykonávání kódu, dokud není připojeno USB a konstruktor je blokující. To může být v mnoha případech nežádoucí.

```cpp
USBSerial usb;
```

Vhodnější může být volba, aby USB konstruktor neblokoval kód a dosadit produktové kódy ručně.

```cpp
USBSerial usb(0x1f00, 0x2012, 0x0001, false);
```

V případě USB se narozdíl od sériové linky nenastavuje baudová rychlost.

# Připojení ze strany PC

Ze strany PC se zařízení hlásí stejně jako každá jiná sériová linka. Viz \[\[[https://wiki.byzance.cz/wiki/doku.php?id=tutorial:serial\|návod](https://wiki.byzance.cz/wiki/doku.php?id=tutorial:serial|návod) na připojení sériové linky\]\].

# Ukázkový kód

Kód pro výpis ''hello world'' pomocí USB

```cpp
USBSerial usb;

void loop(){
   usb.printf("hello world\n");
   Thread::wait(500);
}
```



