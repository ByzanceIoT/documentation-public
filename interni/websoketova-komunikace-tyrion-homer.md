## Komunikační JSON Objekty Mezi Tyrionem a Homerem ###=

----

### Homer na RPi ###

----

###Zjištění stavu zařízení###
**Request:**
```
 {
   "messageType"    : "getState",
   "messageId"      : "SOME ID",
   "messageChannel" : "tyrion"
 }
```
**Reply:**
```
 {
   "messageType"    : "getState",
   "messageId"      : "SOME ID",
   "messageChannel" : "tyrion",
   "status"         : "success/error",
   "error"          : "SOME ERROR MESSAGE", // pouze pokud je status == error
   // následuící - pouze pokud je status == success
   "yodaDeviceId"   : "SOME DEVICE ID",
   "programId"      : "SOME PROGRAM ID"|null,
   "yodaState"      : "ok/error/busy",
   "yodaStateInfo"  : { // pouze pokud je yodaState == ok
       "BUILD_ID"   : "SOME BUILD ID"
   }
   
 }
```

----

###Nahrátí nové isntance B_Programu###
**Request:**
```
 {
   "messageType"    : "loadProgram",
   "messageId"      : "SOME ID",
   "messageChannel" : "tyrion",
   "programId"      : "SOME PROGRAM ID",
   "program"        : "SOME BLOCKO JSON DATA AS STRING"
 }
```
**Reply:**
```
 {
   "messageType"    : "loadProgram",
   "messageId"      : "SOME ID",
   "messageChannel" : "tyrion",
   "status"         : "success/error",
   "error"          : "SOME ERROR MESSAGE" // pouze pokud je status == error
 }
```

----

###Aktualizace firmware HW### 
**Request:**
```
 {
   "messageType"    : "updateYodaFirmware|updateYodaBackup|updateYodaBootloader|updateDeviceFirmware|updateDeviceBootloader",
   "messageId"      : "SOME_ID",
   "messageChannel" : "tyrion",
   "deviceId"       : "1234FEDC",  // HW který se má updatovat tímto binary codem - není potřeba u Yody
   "base64Binary"   : "SOME BINARY DATA IN BASE64"
 }
```
**Reply:**
```
 {
   "messageType"    : "updateYodaFirmware|updateYodaBackup|updateYodaBootloader|updateDeviceFirmware|updateDeviceBootloader",
   "messageId"      : "SOME ID",
   "messageChannel" : "tyrion",
   "status"         : "success/error",
   "error"          : "SOME ERROR MESSAGE" // pouze pokud je status == error
 }
```
**TODO**:// reportování stavu updatu//

----

###Získání seznamu zařízení### 
**Request:**
```
 {
   "messageType"    : "getDeviceList",
   "messageId"      : "SOME_ID",
   "messageChannel" : "tyrion"
 }
```
**Reply:**
```
 {
   "messageType"    : "getDeviceList",
   "messageId"      : "SOME ID",
   "messageChannel" : "tyrion",
   "status"         : "success/error",
   "error"          : "SOME ERROR MESSAGE", // pouze pokud je status == error
   "deviceList"     : ["72E45408","3505ED67"] // pouze pokud je status == success
 }
```

----

###Odebírání TheGrid změn (kanálu the-grid)### 
**Request:**
```
 {
   "messageType"    : "subscribeChannel",
   "messageId"      : "SOME ID",
   "messageChannel" : "the-grid"
 }
```
**Reply:**
```
 {
   "messageType"    : "subscribeChannel",
   "messageId"      : "SOME ID",
   "messageChannel" : "the-grid",
   "status"         : "success/error",
   "error"          : "SOME ERROR MESSAGE", // pouze pokud je status == error
 }
```

----

###Zrušení odběru TheGrid změn (kanálu the-grid)### 
**Request:**
```
 {
   "messageType"    : "unSubscribeChannel",
   "messageId"      : "SOME ID",
   "messageChannel" : "the-grid"
 }
```
**Reply:**
```
 {
   "messageType"    : "unSubscribeChannel",
   "messageId"      : "SOME ID",
   "messageChannel" : "the-grid",
   "status"         : "success/error",
   "error"          : "SOME ERROR MESSAGE", // pouze pokud je status == error
 }
```

----

###Zjištění stavu odběru TheGrid změn (kanálu the-grid)### 
**Request:**
```
 {
   "messageType"    : "isSubscribingChannel",
   "messageId"      : "SOME ID",
   "messageChannel" : "the-grid"
 }
```
**Reply:**
```
 {
   "messageType"    : "isSubscribingChannel",
   "messageId"      : "SOME ID",
   "messageChannel" : "the-grid",
   "status"         : "success/error",
   "error"          : "SOME ERROR MESSAGE", // pouze pokud je status == error
   "subscribing"    : true/false // pouze pokud je status == success
 }
```

----

###Odebírání Remote View změn (kanálu becki)### 
**Request:**
```
 {
   "messageType"    : "subscribeChannel",
   "messageId"      : "SOME ID",
   "messageChannel" : "becki"
 }
```
**Reply:**
```
 {
   "messageType"    : "subscribeChannel",
   "messageId"      : "SOME ID",
   "messageChannel" : "becki",
   "status"         : "success/error",
   "error"          : "SOME ERROR MESSAGE", // pouze pokud je status == error
 }
```

----

###Zrušení odběru Remote View změn (kanálu becki)### 
**Request:**
```
 {
   "messageType"    : "unSubscribeChannel",
   "messageId"      : "SOME ID",
   "messageChannel" : "becki"
 }
```
**Reply:**
```
 {
   "messageType"    : "unSubscribeChannel",
   "messageId"      : "SOME ID",
   "messageChannel" : "becki",
   "status"         : "success/error",
   "error"          : "SOME ERROR MESSAGE", // pouze pokud je status == error
 }
```

----

###Zjištění stavu odběru Remote View změn (kanálu becki)### 
**Request:**
```
 {
   "messageType"    : "isSubscribingChannel",
   "messageId"      : "SOME ID",
   "messageChannel" : "becki"
 }
```
**Reply:**
```
 {
   "messageType"    : "isSubscribingChannel",
   "messageId"      : "SOME ID",
   "messageChannel" : "becki",
   "status"         : "success/error",
   "error"          : "SOME ERROR MESSAGE", // pouze pokud je status == error
   "subscribing"    : true/false // pouze pokud je status == success
 }
```

----

### Homer v homer-serveru ###

Fungují zde všechny předchozí příkazy, pouze s nutností zaslání **"instanceId" v requestu**.

----

###Vytvoření instance### 
**Request:**
```
 {
   "messageType"    : "createInstance",
   "messageId"      : "SOME ID",
   "messageChannel" : "homer-server",
   "instanceId"     : "SOME INSTANCE ID",
   "yodaDeviceId"   : "SOME DEVICE ID"
 }
```
**Reply:**
```
 {
   "messageType"    : "createInstance",
   "messageId"      : "SOME ID",
   "messageChannel" : "homer-server",
   "instanceId"     : "SOME INSTANCE ID",
   "status"         : "success/error",
   "error"          : "SOME ERROR MESSAGE" // pouze pokud je status == error
 }
```

----

###Odstranění instance### 
**Request:**
```
 {
   "messageType"    : "destroyInstance",
   "messageId"      : "SOME ID",
   "messageChannel" : "homer-server",
   "instanceId"     : "SOME INSTANCE ID"
 }
```
**Reply:**
```
 {
   "messageType"    : "destroyInstance",
   "messageId"      : "SOME ID",
   "messageChannel" : "homer-server",
   "instanceId"     : "SOME INSTANCE ID",
   "status"         : "success/error",
   "error"          : "SOME ERROR MESSAGE" // pouze pokud je status == error
 }
```

----

###Seznam instancí### 
**Request:**
```
 {
   "messageType"    : "listInstances",
   "messageId"      : "SOME ID",
   "messageChannel" : "homer-server"
 }
```
**Reply:**
```
 {
   "messageType"    : "listInstances",
   "messageId"      : "SOME ID",
   "messageChannel" : "homer-server"
   "status"         : "success/error",
   "error"          : "SOME ERROR MESSAGE", // pouze pokud je status == error
   "instances"      : ["SOME INSTANCE ID", "SOME INSTANCE ID 2"] // pouze pokud je status == success
 }
```

----

###Ověření existence instance### 
**Request:**
```
 {
   "messageType"    : "instanceExist",
   "messageId"      : "SOME ID",
   "messageChannel" : "homer-server",
   "instanceId"     : "SOME INSTANCE ID"
 }
```
**Reply:**
```
 {
   "messageType"    : "instanceExist",
   "messageId"      : "SOME ID",
   "messageChannel" : "homer-server",
   "instanceId"     : "SOME INSTANCE ID",
   "status"         : "success/error",
   "error"          : "SOME ERROR MESSAGE", // pouze pokud je status == error
   "exist"          : true/false // pouze pokud je status == success
 }
```

###Připojení Yody### 
**homer-server pošle message:**
```
 {
   "messageType"    : "yodaConnected",
   "messageId"      : "SOME ID",
   "messageChannel" : "homer-server",
   "yodaDeviceId"   : "SOME DEVICE ID",
   "instanceId"     : "SOME INSTANCE ID", // pouze pokud má yoda vytvořenou instanci
   "state"          : {
       "BUILD_ID"   : "SOME BUILD ID"
   }
 }
```

###Odpojení Yody### 
**homer-server pošle message:**
```
 {
   "messageType"    : "yodaDisconnected",
   "messageId"      : "SOME ID",
   "messageChannel" : "homer-server",
   "yodaDeviceId"   : "SOME DEVICE ID",
   "instanceId"     : "SOME INSTANCE ID" // pouze pokud má yoda vytvořenou instanci
 }
```

----

### Seznam typů zpráv ###

----

###the-grid kanál### 

**Kanálem můžou chodit následující messageType (opačným směrem volitelně potvrzení):**
  * **TheGrid > Homer**: setDigitalValue, setAnalogValue, setMessage, getValues
  * **Homer > TheGrid**: newDigitalValue, newAnalogValue, newMessage

**Parametry:**
  * **getValues**: digital, analog
  * **setDigitalValue**: targetId, interfaceName, value
  * **setAnalogValue**: targetId, interfaceName, value
  * **setMessage**: targetId, interfaceName, value
  * **newDigitalValue**: targetId, interfaceName, value
  * **newAnalogValue**: targetId, interfaceName, value
  * **newMessage**: targetId, interfaceName, value


----

###becki kanál### 

**Kanálem můžou chodit následující messageType (opačným směrem volitelně potvrzení):**
  * **Becki > Homer**: getValues
  * **Homer > Becki**: newInputConnectorEvent, newOutputConnectorValue, newExternalInputConnectorEvent, newExternalOutputConnectorEvent

**Parametry:**
  * **getValues**: externalConnector, connector
  * **newInputConnectorEvent**: targetType, targetId, connectorName, value
  * **newOutputConnectorValue**: targetType, targetId, connectorName, value
  * **newExternalInputConnectorEvent**: targetType, targetId, connectorName, value
  * **newExternalOutputConnectorEvent**: targetType, targetId, connectorName, value