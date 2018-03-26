## Offline programování z konzole


#### Obecně 
Syntaxe příkazů pro nahrávání binárek do procesorů pomocí utility ''STM32 ST-LINK Utility''. Obecná syntaxe
IODA:

```
<cesta k utilitě>\ST-LINK_CLI.exe -P <cesta k binarce> <počáteční adresa ve FLASH pameti> <další příkazy>
```

Další příkaz je typicky ''-Rst'' pro restartování procesoru po ukončení zápisu do FLASH paměti.


#### Konkrétně 
IODA FIRMWARE:
```
"C:\Program Files (x86)\STMicroelectronics\STM32 ST-LINK Utility\ST-LINK Utility\ST-LINK_CLI.exe" -P "C:path_to_firmware.bin" 0x08010000 -Rst
```

Yoda bootloader
```
"C:\Program Files (x86)\STMicroelectronics\STM32 ST-LINK Utility\ST-LINK Utility\ST-LINK_CLI.exe" -P "C:\path_to_bootloader.bin" 0x08000000 -Rst
```
