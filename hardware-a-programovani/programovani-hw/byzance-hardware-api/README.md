# Byzance API

Byzance API poskytuje uživateli veškeré funkcionality související s připojením k portálu, informace o připojení k síti/portálu a o stavu probíhajících úloh. Jde především o:

* [Vstupy a výstupy do Portálu](vstupy-a-vystupy-do-portalu.md) - zasílání analogových či digitálních hodnot a řetězců
* Callbacky [Busy ](callback-busy.md)a [připojení](callbacky.md) - informace o změně stavu připojení nebo upozornění na vyšší vytížení procesoru 
* [Odložený restart](odlozeny-restart.md) - je-li vyžádán restart serverem, je možné jej odložit do doby, než bude restartování vhodné
* [Uživatelská makra](uzivatelska-makra.md) - pro zjištění informací o verzi mbed, překladače aj.

## Popis třídy Byzance

```cpp
    /**********************************************
     **********************************************
     **********************************************
     ***
     ***      INIT AND DEINIT
     ***
     ***********************************************
     ***********************************************
     **********************************************/

    /** Initialize Byzance library
     *
     * Initialize Byzance library and run Byzance thread.
     * Function is called automatically.
     *
     * \return 0 -> ok
     * \return otherwise -> eror
     */
    static Byzance_Err_TypeDef init();

    /** Deinitialize Byzance library
     *
     * Not implemented yet
     *
     * \return 0 -> ok
     * \return otherwise -> eror
     */
    static Byzance_Err_TypeDef deinit();

    /**
     *
     * Disable Byzance thread start in pre_init
     *
     */
    static bool set_disabled();

    /**
     *
     * Get Byzance thread state
     *
     * \return false    -> not disabled
     * \return true        -> disabled
     */
    static bool is_disabled();

    /**********************************************
     **********************************************
     **********************************************
     ***
     ***      Version getters
     ***
     ***********************************************
     ***********************************************
     **********************************************/

    /** Get version
     *
     * Get version
     *
     * \return version
     */
    static Byzance_Err_TypeDef get_version(char *val);

    /** Get version major
     *
     * Get version major
     *
     * \return version major
     */
    static Byzance_Err_TypeDef get_version_major(char* val);

    /** Get version minor
     *
     * Get version minor
     *
     * \return version minor
     */
    static Byzance_Err_TypeDef get_version_minor(char* val);

    /** Get version patch
     *
     * Get version patch
     *
     * \return version patch
     */
    static Byzance_Err_TypeDef get_version_patch(char* val);

    /**********************************************
     **********************************************
     **********************************************
     ***
     ***      CONFIGURATOR METHODS RELATED TO BOOTLOADER
     ***
     ***********************************************
     ***********************************************
     **********************************************/

    /** Get flashflag
     *
     * Get flashflag state
     *
     * \return flashflag
     */
    static Byzance_Err_TypeDef get_flashflag(uint32_t *val);

    /** Get autobackup
     *
     * Get autobackup state
     *
     * \return autobackup
     */
    static Byzance_Err_TypeDef get_autobackup(uint32_t *val);

    /** Get blreport
     *
     * Get blreport state
     *
     * \return blreport
     */
    static Byzance_Err_TypeDef get_blreport(uint32_t *val);

    /** Get wdenable
     *
     * Get watchdog state
     *
     * \return wdenable
     */
    static Byzance_Err_TypeDef get_wdenable(uint32_t *val);

    /** Get wdtime
     *
     * Get watchdog time
     *
     * \return wdtime
     */
    static Byzance_Err_TypeDef get_wdtime(uint32_t *val);

    /** Get netsource
     *
     * Get netsource
     *
     * \return netsource
     */
    static Byzance_Err_TypeDef get_netsource(uint32_t *val);

    // configured is always 1
    // launched is always 0

    /** Get alias
     *
     * Get alias set in Homer.
     *
     * \return ASCII alias
     */
    static Byzance_Err_TypeDef get_alias(char *val);

    /** Is firmware trusted?
     *
     * Is firmware trusted?
     * It means if it was connected to servers
     * and has been running for a while without problems?
     *
     * \return true - trusted
     * \return false - not trusted
     */
    static Byzance_Err_TypeDef get_trusted(uint32_t *val);

    /** Backup time
     *
     * Backup time settings
     *
     * \return backuptime
     */
    static Byzance_Err_TypeDef get_backuptime(uint32_t *val);

    /** Webview
     *
     * Webview settings
     *
     * \return webview
     */
    static Byzance_Err_TypeDef get_webview(uint32_t *val);

    /** Webport
     *
     * Webport settings
     *
     * \return webport
     */
    static Byzance_Err_TypeDef get_webport(uint32_t *val);

    /** Get timeoffset
     *
     * Get previously stored time offset from UTC time
     *
     * \return time offset
     */
    static Byzance_Err_TypeDef get_timeoffset(int *val);

    /** Get timesync
     *
     * Is time synchronized
     *
     * \return timesync
     */
    static Byzance_Err_TypeDef get_timesync(uint32_t *val);

    /** Get lowpanbr
     *
     * Get Lowpanbr
     *
     * \return lowpanbr
     */
    static Byzance_Err_TypeDef get_lowpanbr(uint32_t *val);

    /** Restart to bootloader
     *
     * Set restartbl flag -> stay in bootloader after restart
     *
     * \return 0 todo
     */
    static Byzance_Err_TypeDef get_restartbl(uint32_t *val);

    /** Restart to bootloader
     *
     * Set restartbl flag -> stay in bootloader after restart
     *
     * \return 0 todo
     */
    static Byzance_Err_TypeDef set_restartbl(uint32_t val = true);

    /**********************************************
     **********************************************
     **********************************************
     ***
     ***      MISCELLANIOUS METHODS
     ***
     ***********************************************
     ***********************************************
     **********************************************/

    /** Get revision
     *
     * Get hardware revision number
     *
     * \return revision
     */
    static Byzance_Err_TypeDef get_revision(uint32_t *val);

    /** Uptime counter
     *
     * How long is device running from last restart
     *
     * \return uptime
     */
    static Byzance_Err_TypeDef get_uptime(uint32_t* val);

    /** Connected time counter
     *
     * How long is device connected to the Byzance servers
     *
     * \return time
     */
    static Byzance_Err_TypeDef get_connected_time(uint32_t* val);

    /** Get Full ID
     *
     * Get device's unique identifier
     * Originally it's 96 bit long number
     * In this function it's represented as 24 byte ASCII hex string
     *
     * \return Full ID
     */
    static Byzance_Err_TypeDef get_full_id(char* val);

    /** Value of supply voltage
     *
     * Get supply voltage as float number
     *
     * \return supply voltage
     */
    static Byzance_Err_TypeDef get_supply_voltage(float* val);

    /** CPU vref internal voltage
     *
     * Get vref internal voltage
     *
     * \return voltage in volts
     */
    static Byzance_Err_TypeDef get_vref_int(float* val);

    /** CPU core temp
     *
     * Get cpu core temp
     *
     * \return temperature in C
     */
    static Byzance_Err_TypeDef get_core_temp(float* val);

    /** Start or stop LED module
     *
     * Attach LED module to be driven by Byzance thread, or disable it and use LEDs by yourself
     *
     * \param    state - true or false
     * \return    none
     */
    static void led_module(bool state);

    /**********************************************
     **********************************************
     **********************************************
     ***
     ***      CONNECTION RELATED METHODS
     ***
     ***********************************************
     ***********************************************
     **********************************************/

    /** Connect to Homer
     *
     * Start ethernet initialisation and run connect procedure to Homer.
     * Function is called automatically after start
     *
     * \return 0 -> ok
     * \return otherwise -> eror
     */
    static Byzance_Err_TypeDef connect();

    /** Disconnect from Byzance servers
     *
     * Disconnect from Byzance servers.
     * Not tested yet.
     *
     * \return TODO doplnit
     */
    static Byzance_Err_TypeDef disconnect();

    /** Get network interface
     *
     * Get network interface
     *
     * \return interface
     */
    static NetworkInterface** get_itf();

    /** Get IP address
     *
     * Get IPv4 or IPv6 address
     *
     * \return IP address in ASCII format XXX:XXX:XXX:XXX
     */
    static const char* get_ip_address();

    /** Get MAC address
     *
     * Get Ethernet/Wifi/LowPan MAC address
     *
     * \return MAC address in format XX:XX:XX:XX:XX:XX
     */
    static const char* get_mac_address();

    /** Change in link layer
     *
     * Link layer was connected or disconnected
     *
     * \param Pointer to function to call
     *
     */
    static void attach_link_connection_changed(void (*function)(bool));

    /** Change in link layer
     *
     * Link layer was connected or disconnected
     *
     * \param Pointer to object and member function to call
     *
     */
    template<typename T>
    void attach_link_connection_changed(T *object, void (T::*member)(bool)) {
        _link_connection_changed_callback.attach(object, member);
    }

    /** Change in communication client (MQTT)
     *
     * Client could be
     * - disconnected
     * - connected and subscribed
     *
     * \param Pointer to function to call
     *
     */
    static void attach_client_connection_changed(void (*function)(bool));

    /** Change in communication client (MQTT)
     *
     * Client could be
     * - disconnected
     * - connected and subscribed
     *
     * \param Pointer to object and member function to call
     *
     */
    template<typename T>
    static void attach_client_connection_changed(T *object, void (T::*member)(bool)) {
        _client_connection_changed_callback.attach(object, member);
    }

    /** Firmware was updated
     *
     * Firmware has been updated callback
     *
     * \param current version
     *
     */
    static void attach_firmware_changed(void (*function)(char*));

    /** Firmware was updated
     *
     * Firmware has been updated callback
     *
     * \param current version
     *
     */
    template<typename T>
    static void attach_firmware_changed(T *object, void (T::*member)(char*)) {
        _firmware_changed_callback.attach(object, member);
    }

    /**********************************************
     **********************************************
     **********************************************
     ***
     ***      RESTART RELATED METHODS
     ***
     ***********************************************
     ***********************************************
     **********************************************/

    /** Restart device
     *
     * Restart device
     *
     * If it's pending and more time is required, restart can be postponed.
     *
     * \return none
     */
    static void restart(time_t sec = 0);

    /** Postpone restart if it is pending
     *
     * Pending restart can be determined from restart_pending() function
     * of in appropriate callback.
     *
     * If it's pending and more time is required, restart can be postponed.
     *
     * \return none
     */
    static void restart_postpone(time_t sec);

    /** Restart is pending?
     *
     * Check if software restart is scheduled.
     *
     * \return 0 if its not scheduled
     * \return otherwise number of seconds remaining to restart
     */
    static time_t restart_pending();

    /** Restart will follow callback
     *
     * If restart is scheduled, this callback will be automatically called.
     *
     * \param pointer to function to be called
     *
     */
    static void attach_restart_follows(void (*function)(void));

    /** Restart will follow callback
     *
     * If restart is scheduled, this callback will be automatically called.
     *
     * \param pointer to object and member function to be called
     *
     */
    template<typename T>
    static void attach_restart_follows(T *object, void (T::*member)(void)) {
        _restart_follows_callback.attach(object, member);
    }

    /** Binary is busy
     *
     * Callback is called when binary is busy
     * It coud be during update, upload, erase...
     *
     * \param pointer to function to be called
     *
     */
    static void attach_bin_busy(void (*function)(bool));

    /** Binary is busy
     *
     * Callback is called when binary is busy
     * It coud be during update, upload, erase...
     *
     * \param pointer to function to be called
     *
     */
    template<typename T>
    static void attach_bin_busy(T *object, void (T::*member)(bool)) {
        _bin_busy_callback.attach(object, member);
    }

    /** get_stack_size
     *
     * TODO add long description
     *
     * \return TODO doplnit
     */
    static uint32_t get_stack_size(void);

    /** get_free_stack
     *
     * TODO add long description
     *
     * \return TODO doplnit
     */
    static uint32_t get_free_stack(void);

    /** get_used_stack
     *
     * TODO add long description
     *
     * \return TODO doplnit
     */
    static uint32_t get_used_stack(void);

    /** get_max_stack
     *
     * TODO add long description
     *
     * \return TODO doplnit
     */
    static uint32_t get_max_stack(void);

    /** get_state
     *
     * TODO add long description
     *
     * \return TODO doplnit
     */
    static Thread::State get_state(void);

    /** get_priority
     *
     * TODO add long description
     *
     * \return TODO doplnit
     */
    static osPriority get_priority(void);

    /** get_connected_link
     *
     * TODO add long description
     *
     * \return TODO doplnit
     */
    static bool get_connected_link(void);
```

