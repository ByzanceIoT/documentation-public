# Byzance API

Veřejné Byzance funkce pomáhají běžnému uživateli zjišťovat stavy zařízení a související události. Společně s \[\[tutorial:mbed\|MBED\]\], \[\[tutorial:macros\|užitečnými makry\]\] a \[\[tutorial:byzance\_io\|Byzance vstupy a výstupy\]\] by měly sloužit jako základní jednotka stavby kódu. Možný příklad použití je dostupný na stránce se \[\[tutorial:structure\|strukturou programu\]\].



&lt;code&gt;

/\*\* Initialize Byzance library

 \*

 \* Initialize Byzance library and run Byzance thread.

 \* Function is called automatically.

 \*

 \* @return 0 -&gt; ok

 \* @return otherwise -&gt; eror

 \*/

static Byzance\_Err\_TypeDef init\(\);

&lt;/code&gt;

&lt;code&gt;

/\*\* Deinitialize Byzance library

 \*

 \* Not implemented yet

 \*

 \* @return 0 -&gt; ok

 \* @return otherwise -&gt; eror

 \*/

static Byzance\_Err\_TypeDef deinit\(\);

&lt;/code&gt;

&lt;code&gt;

/\*\* Connect to Homer

 \*

 \* Start ethernet initialisation and run connect procedure to Homer.

 \* Function is called automatically.

 \*

 \* @return 0 -&gt; ok

 \* @return otherwise -&gt; eror

 \*/

static Byzance\_Err\_TypeDef connect\(\);

&lt;/code&gt;

&lt;code&gt;

/\*\* Disconnect from Byzance servers

 \*

 \* Disconnect from Byzance servers.

 \* Not tested yet.

 \*

 \* @return TODO doplnit

 \*/

static Byzance\_Err\_TypeDef disconnect\(\);

&lt;/code&gt;

&lt;code&gt;

/\*\* Get alias

 \*

 \* Get alias set in Homer.

 \*

 \* @return ASCII alias

 \*/

static const char\* get\_alias\(\);

&lt;/code&gt;

&lt;code&gt;

/\*\* Get IP address

 \*

 \* Get IPv4 or IPv6 address

 \*

 \* @return IP address in ASCII format XXX:XXX:XXX:XXX

 \*/

static const char\* get\_ip\_address\(\);

&lt;/code&gt;

&lt;code&gt;

/\*\* Get MAC address

 \*

 \* Get Ethernet/Wifi/LowPan MAC address

 \*

 \* @return MAC address in format XX:XX:XX:XX:XX:XX

 \*/

static const char\* get\_mac\_address\(\);

&lt;/code&gt;

&lt;code&gt;

/\*\* Is firmware trusted?

 \*

 \* Is firmware trusted?

 \* It means if it was connected to servers

 \* and has been running for a while without problems?

 \*

 \* @return true - trusted

 \* @return false - not trusted

 \*/

static bool get\_trusted\(\);

&lt;/code&gt;

&lt;code&gt;

/\*\* Postpone restart if it is pending

 \*

 \* Pending restart can be determined from restart\_pending\(\) function

 \* of in appropriate callback.

 \*

 \* If it's pending and more time is required, restart can be postponed.

 \*

 \* @return none

 \*/

static void restart\_postpone\(time\_t sec\);

&lt;/code&gt;

&lt;code&gt;

/\*\* Restart is pending?

 \*

 \* Check if software restart is scheduled.

 \*

 \* @return 0 if its not scheduled

 \* @return otherwise number of seconds remaining to restart

 \*/

static time\_t restart\_pending\(\);

&lt;/code&gt;

&lt;code&gt;

/\*\* Start or stop LED module

 \*

 \* Attach LED module to be driven by Byzance thread, or disable it and use LEDs by yourself

 \*

 \* @param	state - true or false

 \* @return	none

 \*/

static void led\_module\(bool state\);

&lt;/code&gt;

&lt;code&gt;

/\*\* Set some value to digital output

 \*

 \* This digital output is visible in Blocko

 \*

 \* @param name registered name

 \* @param value given value

 \*/

static void digital\_output\_set\_value\(const char \*name, bool value\);

&lt;/code&gt;

&lt;code&gt;

/\*\* Set some value to analog output

 \*

 \* This analog output is visible in Blocko

 \*

 \* @param name registered name

 \* @param value given value

 \*/

static void analog\_output\_set\_value\(const char \*name, float value\);

&lt;/code&gt;

&lt;code&gt;

/\*\* Set some value to message output

 \*

 \* This message output is visible in Blocko

 \*

 \* @param name registered name

 \* @param serializer TODO doplnit

 \*/

static void message\_output\_set\_value\(const char \*name, ByzanceSerializer\* serializer\);

&lt;/code&gt;

&lt;code&gt;

/\*\* Change in link layer

 \*

 \* Link layer was connected or disconnected

 \*

 \* @param Pointer to function to call

 \*

 \*/

static void attach\_link\_connection\_changed\(void \(\*function\)\(bool\)\);

&lt;/code&gt;

&lt;code&gt;

/\*\* Change in link layer

 \*

 \* Link layer was connected or disconnected

 \*

 \* @param Pointer to object and member function to call

 \*

 \*/

template&lt;typename T&gt;

void attach\_link\_connection\_changed\(T \*object, void \(T::\*member\)\(bool\)\) {

	\_link\_connection\_changed\_callback.attach\(object, member\);

}

&lt;/code&gt;

&lt;code&gt;

/\*\* Change in communication client \(MQTT\)

 \*

 \* Client could be

 \* - disconnected

 \* - connected and subscribed

 \*

 \* @param Pointer to function to call

 \*

 \*/

static void attach\_client\_connection\_changed\(void \(\*function\)\(bool\)\);

&lt;/code&gt;

&lt;code&gt;

/\*\* Change in communication client \(MQTT\)

 \*

 \* Client could be

 \* - disconnected

 \* - connected and subscribed

 \*

 \* @param Pointer to object and member function to call

 \*

 \*/

template&lt;typename T&gt;

static void attach\_client\_connection\_changed\(T \*object, void \(T::\*member\)\(bool\)\) {

	\_client\_connection\_changed\_callback.attach\(object, member\);

}

&lt;/code&gt;

&lt;code&gt;

/\*\* Byzance state changed

 \*

 \* TODO probably will be reworked

 \*

 \* @param Pointer to function to call

 \*

 \*/

static void attach\_byzance\_state\_changed\(void \(\*function\)\(State\_t\)\);

&lt;/code&gt;

&lt;code&gt;

/\*\* Byzance state changed

 \*

 \* TODO probably will be reworked

 \*

 \* @param Pointer to object and member function to call

 \*

 \*/

template&lt;typename T&gt;

static void attach\_byzance\_state\_changed\(T \*object, void \(T::\*member\)\(State\_t\)\) {

	\_byzance\_state\_changed\_callback.attach\(object, member\);

}

&lt;/code&gt;

&lt;code&gt;

/\*\* Restart will follow callback

 \*

 \* If restart is scheduled, this callback will be automatically called.

 \*

 \* @param pointer to function to be called

 \*

 \*/

static void attach\_restart\_follows\(void \(\*function\)\(void\)\);

&lt;/code&gt;

&lt;code&gt;

/\*\* Restart will follow callback

 \*

 \* If restart is scheduled, this callback will be automatically called.

 \*

 \* @param pointer to object and member function to be called

 \*

 \*/

template&lt;typename T&gt;

static void attach\_restart\_pending\(T \*object, void \(T::\*member\)\(void\)\) {

	\_restart\_follows\_callback.attach\(object, member\);

}

&lt;/code&gt;

