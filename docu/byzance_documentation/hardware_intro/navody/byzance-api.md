# Byzance API

Veřejné Byzance funkce pomáhají běžnému uživateli zjišťovat stavy zařízení a související události. Společně s \[\[tutorial:mbed\|MBED\]\], \[\[tutorial:macros\|užitečnými makry\]\] a \[\[tutorial:byzance\_io\|Byzance vstupy a výstupy\]\] by měly sloužit jako základní jednotka stavby kódu. Možný příklad použití je dostupný na stránce se \[\[tutorial:structure\|strukturou programu\]\].

```cpp
/** Initialize Byzance library
*
* Initialize Byzance library and run Byzance thread.
* Function is called automatically.
*
* @return 0 -> ok
* @return otherwise -> eror
*/
static Byzance_Err_TypeDef init();
```

```cpp
/** Deinitialize Byzance library
*
* Not implemented yet
*
* @return 0 -> ok
* @return otherwise -> eror
*/
static Byzance_Err_TypeDef deinit();
```

```cpp
/** Connect to Homer
*
* Start ethernet initialisation and run connect procedure to Homer.
* Function is called automatically.
*
* @return 0 -> ok
* @return otherwise -> eror
*/
static Byzance_Err_TypeDef connect();
```

```cpp
/** Disconnect from Byzance servers
*
* Disconnect from Byzance servers.
* Not tested yet.
*
* @return TODO doplnit
*/
static Byzance_Err_TypeDef disconnect();
```

```cpp
/** Get alias
*
* Get alias set in Homer.
*
* @return ASCII alias
*/
static const char* get_alias();
```

```cpp
/** Get IP address
*
* Get IPv4 or IPv6 address
*
* @return IP address in ASCII format XXX:XXX:XXX:XXX
*/
static const char* get_ip_address();
```

```cpp
/** Get MAC address
*
* Get Ethernet/Wifi/LowPan MAC address
*
* @return MAC address in format XX:XX:XX:XX:XX:XX
*/
static const char* get_mac_address();
```

```cpp
/** Is firmware trusted?
*
* Is firmware trusted?
* It means if it was connected to servers
* and has been running for a while without problems?
*
* @return true - trusted
* @return false - not trusted
*/
static bool get_trusted();
```

```cpp
/** Postpone restart if it is pending
*
* Pending restart can be determined from restart_pending() function
* of in appropriate callback.
*
* If it's pending and more time is required, restart can be postponed.
*
* @return none
*/
static void restart_postpone(time_t sec);
```

```cpp
/** Restart is pending?
*
* Check if software restart is scheduled.
*
* @return 0 if its not scheduled
* @return otherwise number of seconds remaining to restart
*/
static time_t restart_pending();
```

```cpp
/** Start or stop LED module
*
* Attach LED module to be driven by Byzance thread, or disable it and use LEDs by yourself
*
* @param    state - true or false
* @return    none
*/
static void led_module(bool state);
```

```cpp
/** Set some value to digital output
*
* This digital output is visible in Blocko
*
* @param name registered name
* @param value given value
*/
static void digital_output_set_value(const char *name, bool value);
```

```cpp
/** Set some value to analog output
*
* This analog output is visible in Blocko
*
* @param name registered name
* @param value given value
*/
static void analog_output_set_value(const char *name, float value);
```

```cpp
/** Set some value to message output
*
* This message output is visible in Blocko
*
* @param name registered name
* @param serializer TODO doplnit
*/
static void message_output_set_value(const char *name, ByzanceSerializer* serializer);
```

```cpp
/** Change in link layer
*
* Link layer was connected or disconnected
*
* @param Pointer to function to call
*
*/
static void attach_link_connection_changed(void (*function)(bool));
```

```cpp
/** Change in link layer
*
* Link layer was connected or disconnected
*
* @param Pointer to object and member function to call
*
*/
template<typename T>
void attach_link_connection_changed(T *object, void (T::*member)(bool)) {
    _link_connection_changed_callback.attach(object, member);
}
```

```cpp
/** Change in communication client (MQTT)
*
* Client could be
* - disconnected
* - connected and subscribed
*
* @param Pointer to function to call
*
*/
static void attach_client_connection_changed(void (*function)(bool));
```

```cpp
/** Change in communication client (MQTT)
*
* Client could be
* - disconnected
* - connected and subscribed
*
* @param Pointer to object and member function to call
*
*/
template<typename T>
static void attach_client_connection_changed(T *object, void (T::*member)(bool)) {
    _client_connection_changed_callback.attach(object, member);
}
```

```cpp
/** Byzance state changed
*
* TODO probably will be reworked
*
* @param Pointer to function to call
*
*/
static void attach_byzance_state_changed(void (*function)(State_t));
```

```cpp
/** Byzance state changed
*
* TODO probably will be reworked
*
* @param Pointer to object and member function to call
*
*/
template<typename T>
static void attach_byzance_state_changed(T *object, void (T::*member)(State_t)) {
    _byzance_state_changed_callback.attach(object, member);
}
```

```cpp
/** Restart will follow callback
*
* If restart is scheduled, this callback will be automatically called.
*
* @param pointer to function to be called
*
*/
static void attach_restart_follows(void (*function)(void));
```

```cpp
/** Restart will follow callback
*
* If restart is scheduled, this callback will be automatically called.
*
* @param pointer to object and member function to be called
*
*/
template<typename T>
static void attach_restart_pending(T *object, void (T::*member)(void)) {
    _restart_follows_callback.attach(object, member);
}
```



