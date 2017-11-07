## Offline programování z konzole


#### Obecně 
Syntaxe příkazů pro nahrávání binárek do procesorů pomocí utility ''STM32 ST-LINK Utility''. Obecná syntaxe
YODA:

```
<cesta k utilitě>\ST-LINK_CLI.exe -P <cesta k binarce> <počáteční adresa ve FLASH pameti> <další příkazy>
```

Další příkaz je typicky ''-Rst'' pro restartování procesoru po ukončení zápisu do FLASH paměti.


#### Konkrétně 
YODA:
```
"C:\Program Files (x86)\STMicroelectronics\STM32 ST-LINK Utility\ST-LINK Utility\ST-LINK_CLI.exe" -P "C:\Work\Git\hw-libs\byzance\main.bin" 0x08010000 -Rst
```

Device:
```
"C:\Program Files (x86)\STMicroelectronics\STM32 ST-LINK Utility\ST-LINK Utility\ST-LINK_CLI.exe" -P "C:\Work\Git\hw-libs\buskitG2\main.bin" 0x08004000 -Rst
```

MBED Bootloade device:
```
"C:\Program Files (x86)\STMicroelectronics\STM32 ST-LINK Utility\ST-LINK Utility\ST-LINK_CLI.exe" -P "C:\Work\Git\hw-libs\deviceG2_bootloader\main.bin" 0x08000000 -Rst
```

HAL BOOT DEVICE
```
"C:\Program Files (x86)\STMicroelectronics\STM32 ST-LINK Utility\ST-LINK Utility\ST-LINK_CLI.exe" -P "C:\Work\Git\hw-libs\deviceG2_bootloader_hal\debug\deviceG2_bootloader_hal.bin" 0x08000000 -Rst
```

Yoda bootloader
```
"C:\Program Files (x86)\STMicroelectronics\STM32 ST-LINK Utility\ST-LINK Utility\ST-LINK_CLI.exe" -P "C:\Work\Git\hw-libs\yodaG2_bootloader\main.bin" 0x08000000 -Rst
```
        
DEVICE wireless_shark

```
"C:\Program Files (x86)\STMicroelectronics\STM32 ST-LINK Utility\ST-LINK Utility\ST-LINK_CLI.exe" -P "C:\Work\Git\hw-libs\wireless_shark\main.bin" 0x08004000 -Rst
```
