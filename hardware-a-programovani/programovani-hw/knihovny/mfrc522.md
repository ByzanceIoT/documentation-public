---
search:
  keywords:
    - MFRC522
    - MIFARE_Key
    - Uid
    - PCD_Register
    - PCD_Command
    - PCD_RxGain
    - PICC_Command
    - MIFARE_Misc
    - PICC_Type
    - StatusCode
    - uid
    - FIFO_SIZE
    - MFRC522
    - MFRC522
    - ~MFRC522
    - PCD_Init
    - PCD_Reset
    - PCD_AntennaOn
    - PCD_WriteRegister
    - PCD_WriteRegister
    - PCD_ReadRegister
    - PCD_ReadRegister
    - PCD_SetRegisterBits
    - PCD_ClrRegisterBits
    - PCD_CalculateCRC
    - PCD_TransceiveData
    - PCD_CommunicateWithPICC
    - PICC_RequestA
    - PICC_WakeupA
    - PICC_REQA_or_WUPA
    - PICC_Select
    - PICC_HaltA
    - PCD_Authenticate
    - PCD_StopCrypto1
    - MIFARE_Read
    - MIFARE_Write
    - MIFARE_UltralightWrite
    - MIFARE_Decrement
    - MIFARE_Increment
    - MIFARE_Restore
    - MIFARE_Transfer
    - PCD_MIFARE_Transceive
    - PICC_GetType
    - PICC_GetTypeName
    - GetStatusCodeName
    - MIFARE_SetAccessBits
    - PICC_IsNewCardPresent
    - PICC_ReadCardSerial
---

# MFRC522

## Classes

| Type | Name |
| :--- | :--- |
| struct | [**MIFARE\_Key**](https://github.com/ByzanceIoT/documentation-public/tree/3fe90b10188febdfcd320d169525b1b1c90c932e/hardware-a-programovani/programovani-hw/byzance-api/api/struct_m_f_r_c522_1_1_m_i_f_a_r_e___key.md) |
| struct | [**Uid**](https://github.com/ByzanceIoT/documentation-public/tree/3fe90b10188febdfcd320d169525b1b1c90c932e/hardware-a-programovani/programovani-hw/byzance-api/api/struct_m_f_r_c522_1_1_uid.md) |

## Public Types

| Type | Name |
| :--- | :--- |
| enum | [**PCD\_Register**](mfrc522.md#1ae3b374c61bf50256289349fdb78fe181) { **CommandReg** = 0x01, **ComIEnReg** = 0x02, **DivIEnReg** = 0x03, **ComIrqReg** = 0x04, **DivIrqReg** = 0x05, **ErrorReg** = 0x06, **Status1Reg** = 0x07, **Status2Reg** = 0x08, **FIFODataReg** = 0x09, **FIFOLevelReg** = 0x0A, **WaterLevelReg** = 0x0B, **ControlReg** = 0x0C, **BitFramingReg** = 0x0D, **CollReg** = 0x0E, **ModeReg** = 0x11, **TxModeReg** = 0x12, **RxModeReg** = 0x13, **TxControlReg** = 0x14, **TxASKReg** = 0x15, **TxSelReg** = 0x16, **RxSelReg** = 0x17, **RxThresholdReg** = 0x18, **DemodReg** = 0x19, **MfTxReg** = 0x1C, **MfRxReg** = 0x1D, **SerialSpeedReg** = 0x1F, **CRCResultRegH** = 0x21, **CRCResultRegL** = 0x22, **ModWidthReg** = 0x24, **RFCfgReg** = 0x26, **GsNReg** = 0x27, **CWGsPReg** = 0x28, **ModGsPReg** = 0x29, **TModeReg** = 0x2A, **TPrescalerReg** = 0x2B, **TReloadRegH** = 0x2C, **TReloadRegL** = 0x2D, **TCntValueRegH** = 0x2E, **TCntValueRegL** = 0x2F, **TestSel1Reg** = 0x31, **TestSel2Reg** = 0x32, **TestPinEnReg** = 0x33, **TestPinValueReg** = 0x34, **TestBusReg** = 0x35, **AutoTestReg** = 0x36, **VersionReg** = 0x37, **AnalogTestReg** = 0x38, **TestDAC1Reg** = 0x39, **TestDAC2Reg** = 0x3A, **TestADCReg** = 0x3B } |
| enum | [**PCD\_Command**](mfrc522.md#1a973011639bbee6ad7035ae4dd49e2e07) { **PCD\_Idle** = 0x00, **PCD\_Mem** = 0x01, **PCD\_GenerateRandomID** = 0x02, **PCD\_CalcCRC** = 0x03, **PCD\_Transmit** = 0x04, **PCD\_NoCmdChange** = 0x07, **PCD\_Receive** = 0x08, **PCD\_Transceive** = 0x0C, **PCD\_MFAuthent** = 0x0E, **PCD\_SoftReset** = 0x0F } |
| enum | [**PCD\_RxGain**](mfrc522.md#1ab7e2bdb063a8ab5f8f29bd05e6867335) { **RxGain\_18dB** = 0x00 &lt;&lt; 4, **RxGain\_23dB** = 0x01 &lt;&lt; 4, **RxGain\_18dB\_2** = 0x02 &lt;&lt; 4, **RxGain\_23dB\_2** = 0x03 &lt;&lt; 4, **RxGain\_33dB** = 0x04 &lt;&lt; 4, **RxGain\_38dB** = 0x05 &lt;&lt; 4, **RxGain\_43dB** = 0x06 &lt;&lt; 4, **RxGain\_48dB** = 0x07 &lt;&lt; 4, **RxGain\_min** = 0x00 &lt;&lt; 4, **RxGain\_avg** = 0x04 &lt;&lt; 4, **RxGain\_max** = 0x07 &lt;&lt; 4 } |
| enum | [**PICC\_Command**](mfrc522.md#1a5d46a0e2b34b21f51f40ea95795b5e49) { **PICC\_CMD\_REQA** = 0x26, **PICC\_CMD\_WUPA** = 0x52, **PICC\_CMD\_CT** = 0x88, **PICC\_CMD\_SEL\_CL1** = 0x93, **PICC\_CMD\_SEL\_CL2** = 0x95, **PICC\_CMD\_SEL\_CL3** = 0x97, **PICC\_CMD\_HLTA** = 0x50, **PICC\_CMD\_MF\_AUTH\_KEY\_A** = 0x60, **PICC\_CMD\_MF\_AUTH\_KEY\_B** = 0x61, **PICC\_CMD\_MF\_READ** = 0x30, **PICC\_CMD\_MF\_WRITE** = 0xA0, **PICC\_CMD\_MF\_DECREMENT** = 0xC0, **PICC\_CMD\_MF\_INCREMENT** = 0xC1, **PICC\_CMD\_MF\_RESTORE** = 0xC2, **PICC\_CMD\_MF\_TRANSFER** = 0xB0, **PICC\_CMD\_UL\_WRITE** = 0xA2 } |
| enum | [**MIFARE\_Misc**](mfrc522.md#1a92c17a5b83cc4fde3cc3454c03b8eede) { **MF\_ACK** = 0xA, **MF\_KEY\_SIZE** = 6 } |
| enum | [**PICC\_Type**](mfrc522.md#1a3d8d44527557fe596a9ac486d49239de) { **PICC\_TYPE\_UNKNOWN** = 0, **PICC\_TYPE\_ISO\_14443\_4** = 1, **PICC\_TYPE\_ISO\_18092** = 2, **PICC\_TYPE\_MIFARE\_MINI** = 3, **PICC\_TYPE\_MIFARE\_1K** = 4, **PICC\_TYPE\_MIFARE\_4K** = 5, **PICC\_TYPE\_MIFARE\_UL** = 6, **PICC\_TYPE\_MIFARE\_PLUS** = 7, **PICC\_TYPE\_TNP3XXX** = 8, **PICC\_TYPE\_NOT\_COMPLETE** = 255 } |
| enum | [**StatusCode**](mfrc522.md#1ac0da61f475014ccb8c77205287a09c27) { **STATUS\_OK** = 1, **STATUS\_ERROR** = 2, **STATUS\_COLLISION** = 3, **STATUS\_TIMEOUT** = 4, **STATUS\_NO\_ROOM** = 5, **STATUS\_INTERNAL\_ERROR** = 6, **STATUS\_INVALID** = 7, **STATUS\_CRC\_WRONG** = 8, **STATUS\_MIFARE\_NACK** = 9 } |

## Public Attributes

| Type | Name |
| :--- | :--- |
| [**Uid**](https://github.com/ByzanceIoT/documentation-public/tree/3fe90b10188febdfcd320d169525b1b1c90c932e/hardware-a-programovani/programovani-hw/byzance-api/api/struct_m_f_r_c522_1_1_uid.md) | [**uid**](mfrc522.md#1ad456545d41962dd7f8bd4210f5618498) |

## Public Static Attributes

| Type | Name |
| :--- | :--- |
| static const uint8\_t | [**FIFO\_SIZE**](mfrc522.md#1a45b3d611adc98970d1b11848f84bfdda) |

## Public Functions

| Type | Name |
| :--- | :--- |
|  | [**MFRC522**](mfrc522.md#1ade858e2bc1fdcb3986ac0166a3a8c431) \(PinName sda, PinName scl, uint32\_t frequency = 400000\) |
|  | [**MFRC522**](mfrc522.md#1a1d945f8c15c00b1b86d9059efd6eaf2c) \(PinName sda, PinName scl, PinName reset\) |
|  | [**~MFRC522**](mfrc522.md#1a864a3473182f9c76fe5b3ec1f6c91e20) \(\) |
| int | [**PCD\_Init**](mfrc522.md#1a796cbcfd8eea12f7c27d044304d08fb6) \(void\) |
| int | [**PCD\_Reset**](mfrc522.md#1a4c0f9930a427dc2513a55c219c80b509) \(void\) |
| int | [**PCD\_AntennaOn**](mfrc522.md#1ac78f9bd7069b1bccd708ec489bbd1277) \(void\) |
| int | [**PCD\_WriteRegister**](mfrc522.md#1ac6427b6bc6ffd7dc8f68d4dffde9722c) \(uint8\_t reg, uint8\_t value\) |
| int | [**PCD\_WriteRegister**](mfrc522.md#1a25daa50c8111e54628db4ac50292837d) \(uint8\_t reg, uint8\_t count, uint8\_t \* values\) |
| uint8\_t | [**PCD\_ReadRegister**](mfrc522.md#1a0e064bcccc1a859a258a56c066f98758) \(uint8\_t reg\) |
| void | [**PCD\_ReadRegister**](mfrc522.md#1a1c64025265eff9a33bf6ae8a62cb102d) \(uint8\_t reg, uint8\_t count, uint8\_t \* values, uint8\_t rxAlign = 0\) |
| void | [**PCD\_SetRegisterBits**](mfrc522.md#1a5aa29681ea594964b89a048a8fe715b9) \(uint8\_t reg, uint8\_t mask\) |
| void | [**PCD\_ClrRegisterBits**](mfrc522.md#1a6b15e83eedc2ac55deeb57ba205511b5) \(uint8\_t reg, uint8\_t mask\) |
| uint8\_t | [**PCD\_CalculateCRC**](mfrc522.md#1aa94628b24de2a9c0a2626a8382704a54) \(uint8\_t \* data, uint8\_t length, uint8\_t \* result\) |
| uint8\_t | [**PCD\_TransceiveData**](mfrc522.md#1a75cc89dab5f3a003f04826dea97203fb) \(uint8\_t \* sendData, uint8\_t sendLen, uint8\_t \* backData, uint8\_t \* backLen, uint8\_t \* validBits = NULL, uint8\_t rxAlign = 0, bool checkCRC = false\) |
| uint8\_t | [**PCD\_CommunicateWithPICC**](mfrc522.md#1aee9b9e014516a55ea0c9c75d93cced27) \(uint8\_t command, uint8\_t waitIRq, uint8\_t \* sendData, uint8\_t sendLen, uint8\_t \* backData = NULL, uint8\_t \* backLen = NULL, uint8\_t \* validBits = NULL, uint8\_t rxAlign = 0, bool checkCRC = false\) |
| uint8\_t | [**PICC\_RequestA**](mfrc522.md#1a3a93f92bf2b4c1fa6f3d76fd97a65190) \(uint8\_t \* bufferATQA, uint8\_t \* bufferSize\) |
| uint8\_t | [**PICC\_WakeupA**](mfrc522.md#1a023b78fa99f1f0c8acd154584e3daa25) \(uint8\_t \* bufferATQA, uint8\_t \* bufferSize\) |
| uint8\_t | [**PICC\_REQA\_or\_WUPA**](mfrc522.md#1a8b21b66da01172854c66def59fe9d07b) \(uint8\_t command, uint8\_t \* bufferATQA, uint8\_t \* bufferSize\) |
| uint8\_t | [**PICC\_Select**](mfrc522.md#1a5d84996eaafe4ded4edca5bd4383c865) \([**Uid**](https://github.com/ByzanceIoT/documentation-public/tree/3fe90b10188febdfcd320d169525b1b1c90c932e/hardware-a-programovani/programovani-hw/byzance-api/api/struct_m_f_r_c522_1_1_uid.md) \* uid, uint8\_t validBits = 0\) |
| uint8\_t | [**PICC\_HaltA**](mfrc522.md#1ad5e79247f02c1abf4f7fb1ade26e6428) \(void\) |
| uint8\_t | [**PCD\_Authenticate**](mfrc522.md#1a79f632aec9e2ca7c27fe4208f5d4843e) \(uint8\_t command, uint8\_t blockAddr, [**MIFARE\_Key**](https://github.com/ByzanceIoT/documentation-public/tree/3fe90b10188febdfcd320d169525b1b1c90c932e/hardware-a-programovani/programovani-hw/byzance-api/api/struct_m_f_r_c522_1_1_m_i_f_a_r_e___key.md) \* key, [**Uid**](https://github.com/ByzanceIoT/documentation-public/tree/3fe90b10188febdfcd320d169525b1b1c90c932e/hardware-a-programovani/programovani-hw/byzance-api/api/struct_m_f_r_c522_1_1_uid.md) \* uid\) |
| void | [**PCD\_StopCrypto1**](mfrc522.md#1a087a46833537cab757014e5b01afe4f6) \(void\) |
| uint8\_t | [**MIFARE\_Read**](mfrc522.md#1a2dbf95655f78503a119f30b3507cebcf) \(uint8\_t blockAddr, uint8\_t \* buffer, uint8\_t \* bufferSize\) |
| uint8\_t | [**MIFARE\_Write**](mfrc522.md#1a76c49a7d419120273586f145c53baec1) \(uint8\_t blockAddr, uint8\_t \* buffer, uint8\_t bufferSize\) |
| uint8\_t | [**MIFARE\_UltralightWrite**](mfrc522.md#1a01800ec934813f6e89ef9ca3f05d20b2) \(uint8\_t page, uint8\_t \* buffer, uint8\_t bufferSize\) |
| uint8\_t | [**MIFARE\_Decrement**](mfrc522.md#1ac779750e3f056d68aaa1b6a52ea757a9) \(uint8\_t blockAddr, uint32\_t delta\) |
| uint8\_t | [**MIFARE\_Increment**](mfrc522.md#1ad2ff3ec8a7c323a86a4f9769f1bf564f) \(uint8\_t blockAddr, uint32\_t delta\) |
| uint8\_t | [**MIFARE\_Restore**](mfrc522.md#1a26cd9238e46b35e8adcb68acb2127f77) \(uint8\_t blockAddr\) |
| uint8\_t | [**MIFARE\_Transfer**](mfrc522.md#1a44aaaf9a3310fc1c67daddf8733f579b) \(uint8\_t blockAddr\) |
| uint8\_t | [**PCD\_MIFARE\_Transceive**](mfrc522.md#1a6d42d0615c3e956278658cddb487ba09) \(uint8\_t \* sendData, uint8\_t sendLen, bool acceptTimeout = false\) |
| uint8\_t | [**PICC\_GetType**](mfrc522.md#1a827930d1a50d63402d7edcda5a74093d) \(uint8\_t sak\) |
| char \* | [**PICC\_GetTypeName**](mfrc522.md#1ac3b1289ba9a0f0dd4b117071c52a1764) \(uint8\_t type\) |
| char \* | [**GetStatusCodeName**](mfrc522.md#1a4469297fa43eca37db6505ad2922c0f3) \(uint8\_t code\) |
| void | [**MIFARE\_SetAccessBits**](mfrc522.md#1ac82a4d75dd70d25afbd24726e91796b3) \(uint8\_t \* accessBitBuffer, uint8\_t g0, uint8\_t g1, uint8\_t g2, uint8\_t g3\) |
| bool | [**PICC\_IsNewCardPresent**](mfrc522.md#1a2bd3bd7586a52fa107e0e71c7f073eb2) \(void\) |
| bool | [**PICC\_ReadCardSerial**](mfrc522.md#1a3664b1b301d6e740bdab01842622670e) \(void\) |

## Detailed Description

[**MFRC522**](mfrc522.md) example

```cpp
#include "mbed.h"
#include "MFRC522.h"

//KL25Z Pins for MFRC522 SPI interface
#define SPI_MOSI    PTC6
#define SPI_MISO    PTC7
#define SPI_SCLK    PTC5
#define SPI_CS      PTC4
// KL25Z Pin for MFRC522 reset
#define MF_RESET    PTC3
// KL25Z Pins for Debug UART port
#define UART_RX     PTA1
#define UART_TX     PTA2

DigitalOut LedRed   (LED_RED);
DigitalOut LedGreen (LED_GREEN);

Serial     DebugUART(UART_TX, UART_RX);
MFRC522    RfChip   (SPI_MOSI, SPI_MISO, SPI_SCLK, SPI_CS, MF_RESET);

int main(void) {
  // Set debug UART speed
  DebugUART.baud(115200);

  // Init. RC522 Chip
  RfChip.PCD_Init();

  while (true) {
    LedRed   = 1;
    LedGreen = 1;

    // Look for new cards
    if ( ! RfChip.PICC_IsNewCardPresent())
    {
      wait_ms(500);
      continue;
    }

    LedRed   = 0;

    // Select one of the cards
    if ( ! RfChip.PICC_ReadCardSerial())
    {
      wait_ms(500);
      continue;
    }

    LedRed   = 1;
    LedGreen = 0;

    // Print Card UID
    printf("Card UID: ");
    for (uint8_t i = 0; i < RfChip.uid.size; i++)
    {
      printf(" %X02", RfChip.uid.uidByte[i]);
    }
    printf("\n\r");

    // Print Card type
    uint8_t piccType = RfChip.PICC_GetType(RfChip.uid.sak);
    printf("PICC Type: %s \n\r", RfChip.PICC_GetTypeName(piccType));
    wait_ms(1000);
  }
}
```

## Public Types Documentation

### enum [PCD\_Register](mfrc522.md#1ae3b374c61bf50256289349fdb78fe181)

```cpp
enum MFRC522::PCD_Register {
    CommandReg = 0x01,
    ComIEnReg = 0x02,
    DivIEnReg = 0x03,
    ComIrqReg = 0x04,
    DivIrqReg = 0x05,
    ErrorReg = 0x06,
    Status1Reg = 0x07,
    Status2Reg = 0x08,
    FIFODataReg = 0x09,
    FIFOLevelReg = 0x0A,
    WaterLevelReg = 0x0B,
    ControlReg = 0x0C,
    BitFramingReg = 0x0D,
    CollReg = 0x0E,
    ModeReg = 0x11,
    TxModeReg = 0x12,
    RxModeReg = 0x13,
    TxControlReg = 0x14,
    TxASKReg = 0x15,
    TxSelReg = 0x16,
    RxSelReg = 0x17,
    RxThresholdReg = 0x18,
    DemodReg = 0x19,
    MfTxReg = 0x1C,
    MfRxReg = 0x1D,
    SerialSpeedReg = 0x1F,
    CRCResultRegH = 0x21,
    CRCResultRegL = 0x22,
    ModWidthReg = 0x24,
    RFCfgReg = 0x26,
    GsNReg = 0x27,
    CWGsPReg = 0x28,
    ModGsPReg = 0x29,
    TModeReg = 0x2A,
    TPrescalerReg = 0x2B,
    TReloadRegH = 0x2C,
    TReloadRegL = 0x2D,
    TCntValueRegH = 0x2E,
    TCntValueRegL = 0x2F,
    TestSel1Reg = 0x31,
    TestSel2Reg = 0x32,
    TestPinEnReg = 0x33,
    TestPinValueReg = 0x34,
    TestBusReg = 0x35,
    AutoTestReg = 0x36,
    VersionReg = 0x37,
    AnalogTestReg = 0x38,
    TestDAC1Reg = 0x39,
    TestDAC2Reg = 0x3A,
    TestADCReg = 0x3B,
};
```

[**MFRC522**](mfrc522.md) registers \(described in chapter 9 of the datasheet\). When using SPI all addresses areed one bit left in the "SPI address byte" \(section 8.1.2.3\)

### enum [PCD\_Command](mfrc522.md#1a973011639bbee6ad7035ae4dd49e2e07)

```cpp
enum MFRC522::PCD_Command {
    PCD_Idle = 0x00,
    PCD_Mem = 0x01,
    PCD_GenerateRandomID = 0x02,
    PCD_CalcCRC = 0x03,
    PCD_Transmit = 0x04,
    PCD_NoCmdChange = 0x07,
    PCD_Receive = 0x08,
    PCD_Transceive = 0x0C,
    PCD_MFAuthent = 0x0E,
    PCD_SoftReset = 0x0F,
};
```

### enum [PCD\_RxGain](mfrc522.md#1ab7e2bdb063a8ab5f8f29bd05e6867335)

```cpp
enum MFRC522::PCD_RxGain {
    RxGain_18dB = 0x00 << 4,
    RxGain_23dB = 0x01 << 4,
    RxGain_18dB_2 = 0x02 << 4,
    RxGain_23dB_2 = 0x03 << 4,
    RxGain_33dB = 0x04 << 4,
    RxGain_38dB = 0x05 << 4,
    RxGain_43dB = 0x06 << 4,
    RxGain_48dB = 0x07 << 4,
    RxGain_min = 0x00 << 4,
    RxGain_avg = 0x04 << 4,
    RxGain_max = 0x07 << 4,
};
```

### enum [PICC\_Command](mfrc522.md#1a5d46a0e2b34b21f51f40ea95795b5e49)

```cpp
enum MFRC522::PICC_Command {
    PICC_CMD_REQA = 0x26,
    PICC_CMD_WUPA = 0x52,
    PICC_CMD_CT = 0x88,
    PICC_CMD_SEL_CL1 = 0x93,
    PICC_CMD_SEL_CL2 = 0x95,
    PICC_CMD_SEL_CL3 = 0x97,
    PICC_CMD_HLTA = 0x50,
    PICC_CMD_MF_AUTH_KEY_A = 0x60,
    PICC_CMD_MF_AUTH_KEY_B = 0x61,
    PICC_CMD_MF_READ = 0x30,
    PICC_CMD_MF_WRITE = 0xA0,
    PICC_CMD_MF_DECREMENT = 0xC0,
    PICC_CMD_MF_INCREMENT = 0xC1,
    PICC_CMD_MF_RESTORE = 0xC2,
    PICC_CMD_MF_TRANSFER = 0xB0,
    PICC_CMD_UL_WRITE = 0xA2,
};
```

### enum [MIFARE\_Misc](mfrc522.md#1a92c17a5b83cc4fde3cc3454c03b8eede)

```cpp
enum MFRC522::MIFARE_Misc {
    MF_ACK = 0xA,
    MF_KEY_SIZE = 6,
};
```

### enum [PICC\_Type](mfrc522.md#1a3d8d44527557fe596a9ac486d49239de)

```cpp
enum MFRC522::PICC_Type {
    PICC_TYPE_UNKNOWN = 0,
    PICC_TYPE_ISO_14443_4 = 1,
    PICC_TYPE_ISO_18092 = 2,
    PICC_TYPE_MIFARE_MINI = 3,
    PICC_TYPE_MIFARE_1K = 4,
    PICC_TYPE_MIFARE_4K = 5,
    PICC_TYPE_MIFARE_UL = 6,
    PICC_TYPE_MIFARE_PLUS = 7,
    PICC_TYPE_TNP3XXX = 8,
    PICC_TYPE_NOT_COMPLETE = 255,
};
```

### enum [StatusCode](mfrc522.md#1ac0da61f475014ccb8c77205287a09c27)

```cpp
enum MFRC522::StatusCode {
    STATUS_OK = 1,
    STATUS_ERROR = 2,
    STATUS_COLLISION = 3,
    STATUS_TIMEOUT = 4,
    STATUS_NO_ROOM = 5,
    STATUS_INTERNAL_ERROR = 6,
    STATUS_INVALID = 7,
    STATUS_CRC_WRONG = 8,
    STATUS_MIFARE_NACK = 9,
};
```

## Public Attributes Documentation

### variable [uid](mfrc522.md#1ad456545d41962dd7f8bd4210f5618498)

```cpp
Uid MFRC522::uid;
```

## Public Static Attributes Documentation

### variable [FIFO\_SIZE](mfrc522.md#1a45b3d611adc98970d1b11848f84bfdda)

```cpp
const uint8_t MFRC522::FIFO_SIZE;
```

## Public Functions Documentation

### function [MFRC522](mfrc522.md#1ade858e2bc1fdcb3986ac0166a3a8c431)

```cpp
MFRC522::MFRC522 (
    PinName sda,
    PinName scl,
    uint32_t frequency = 400000
)
```

[**MFRC522**](mfrc522.md) constructor

**Parameters:**

* _sda_ I2C sda pin 
* _scl_ I2C scl pin

Constructor. Prepares the output pins.

### function [MFRC522](mfrc522.md#1a1d945f8c15c00b1b86d9059efd6eaf2c)

```cpp
MFRC522::MFRC522 (
    PinName sda,
    PinName scl,
    PinName reset
)
```

[**MFRC522**](mfrc522.md) constructor

**Parameters:**

* _sda_ I2C sda pin 
* _scl_ I2C scl pin 
* _reset_ Reset pin

Constructor. Prepares the output pins.

### function [~MFRC522](mfrc522.md#1a864a3473182f9c76fe5b3ec1f6c91e20)

```cpp
MFRC522::~MFRC522 ()
```

[**MFRC522**](mfrc522.md) destructor Destructor.

### function [PCD\_Init](mfrc522.md#1a796cbcfd8eea12f7c27d044304d08fb6)

```cpp
int MFRC522::PCD_Init (
    void 
)
```

Initializes the [**MFRC522**](mfrc522.md) chip.

### function [PCD\_Reset](mfrc522.md#1a4c0f9930a427dc2513a55c219c80b509)

```cpp
int MFRC522::PCD_Reset (
    void 
)
```

Performs a soft reset on the [**MFRC522**](mfrc522.md) chip and waits for it to be ready again.

### function [PCD\_AntennaOn](mfrc522.md#1ac78f9bd7069b1bccd708ec489bbd1277)

```cpp
int MFRC522::PCD_AntennaOn (
    void 
)
```

Turns the antenna on by enabling pins TX1 and TX2. After a reset these pins disabled.

### function [PCD\_WriteRegister](mfrc522.md#1ac6427b6bc6ffd7dc8f68d4dffde9722c)

```cpp
int MFRC522::PCD_WriteRegister (
    uint8_t reg,
    uint8_t value
)
```

Writes a byte to the specified register in the [**MFRC522**](mfrc522.md) chip. The interface is described in the datasheet section 8.1.2.

**Parameters:**

* _reg_ The register to write to. One of the PCD\_Register enums. 
* _value_ The value to write.

Writes a byte to the specified register in the [**MFRC522**](mfrc522.md) chip. The interface is described in the datasheet section 8.1.2.

### function [PCD\_WriteRegister](mfrc522.md#1a25daa50c8111e54628db4ac50292837d)

```cpp
int MFRC522::PCD_WriteRegister (
    uint8_t reg,
    uint8_t count,
    uint8_t * values
)
```

Writes a number of bytes to the specified register in the [**MFRC522**](mfrc522.md) chip. The interface is described in the datasheet section 8.1.2.

**Parameters:**

* _reg_ The register to write to. One of the PCD\_Register enums. 
* _count_ The number of bytes to write to the register 
* _values_ The values to write. Byte array.

Writes a number of bytes to the specified register in the [**MFRC522**](mfrc522.md) chip. The interface is described in the datasheet section 8.1.2.

### function [PCD\_ReadRegister](mfrc522.md#1a0e064bcccc1a859a258a56c066f98758)

```cpp
uint8_t MFRC522::PCD_ReadRegister (
    uint8_t reg
)
```

Reads a byte from the specified register in the [**MFRC522**](mfrc522.md) chip. The interface is described in the datasheet section 8.1.2.

**Parameters:**

* _reg_ The register to read from. One of the PCD\_Register enums. 

**Returns:**

Register value

Reads a byte from the specified register in the [**MFRC522**](mfrc522.md) chip. The interface is described in the datasheet section 8.1.2.

### function [PCD\_ReadRegister](mfrc522.md#1a1c64025265eff9a33bf6ae8a62cb102d)

```cpp
void MFRC522::PCD_ReadRegister (
    uint8_t reg,
    uint8_t count,
    uint8_t * values,
    uint8_t rxAlign = 0
)
```

Reads a number of bytes from the specified register in the [**MFRC522**](mfrc522.md) chip. The interface is described in the datasheet section 8.1.2.

**Parameters:**

* _reg_ The register to read from. One of the PCD\_Register enums. 
* _count_ The number of bytes to read. 
* _values_ Byte array to store the values in. 
* _rxAlign_ Only bit positions rxAlign..7 in values\[0\] are updated.

Reads a number of bytes from the specified register in the [**MFRC522**](mfrc522.md) chip. The interface is described in the datasheet section 8.1.2.

### function [PCD\_SetRegisterBits](mfrc522.md#1a5aa29681ea594964b89a048a8fe715b9)

```cpp
void MFRC522::PCD_SetRegisterBits (
    uint8_t reg,
    uint8_t mask
)
```

Sets the bits given in mask in register reg.

**Parameters:**

* _reg_ The register to update. One of the PCD\_Register enums. 
* _mask_ The bits to set.

Sets the bits given in mask in register reg.

### function [PCD\_ClrRegisterBits](mfrc522.md#1a6b15e83eedc2ac55deeb57ba205511b5)

```cpp
void MFRC522::PCD_ClrRegisterBits (
    uint8_t reg,
    uint8_t mask
)
```

Clears the bits given in mask from register reg.

**Parameters:**

* _reg_ The register to update. One of the PCD\_Register enums. 
* _mask_ The bits to clear.

Clears the bits given in mask from register reg.

### function [PCD\_CalculateCRC](mfrc522.md#1aa94628b24de2a9c0a2626a8382704a54)

```cpp
uint8_t MFRC522::PCD_CalculateCRC (
    uint8_t * data,
    uint8_t length,
    uint8_t * result
)
```

Use the CRC coprocessor in the [**MFRC522**](mfrc522.md) to calculate a CRC\_A.

**Parameters:**

* _data_ Pointer to the data to transfer to the FIFO for CRC calculation. 
* _length_ The number of bytes to transfer. 
* _result_ Pointer to result buffer. Result is written to result\[0..1\], low byte first. 

**Returns:**

STATUS\_OK on success, STATUS\_??? otherwise.

Use the CRC coprocessor in the [**MFRC522**](mfrc522.md) to calculate a CRC\_A.

### function [PCD\_TransceiveData](mfrc522.md#1a75cc89dab5f3a003f04826dea97203fb)

```cpp
uint8_t MFRC522::PCD_TransceiveData (
    uint8_t * sendData,
    uint8_t sendLen,
    uint8_t * backData,
    uint8_t * backLen,
    uint8_t * validBits = NULL,
    uint8_t rxAlign = 0,
    bool checkCRC = false
)
```

Executes the Transceive command. CRC validation can only be done if backData and backLen are specified.

**Parameters:**

* _sendData_ Pointer to the data to transfer to the FIFO. 
* _sendLen_ Number of bytes to transfer to the FIFO. 
* _backData_ NULL or pointer to buffer if data should be read back after executing the command. 
* _backLen_ Max number of bytes to write to \*backData. Out: The number of bytes returned. 
* _validBits_ The number of valid bits in the last byte. 0 for 8 valid bits. Default NULL. 
* _rxAlign_ Defines the bit position in backData\[0\] for the first bit received. Default 0. 
* _checkCRC_ True =&gt; The last two bytes of the response is assumed to be a CRC\_A that must be validated.

**Returns:**

STATUS\_OK on success, STATUS\_??? otherwise.

Executes the Transceive command. CRC validation can only be done if backData and backLen are specified.

### function [PCD\_CommunicateWithPICC](mfrc522.md#1aee9b9e014516a55ea0c9c75d93cced27)

```cpp
uint8_t MFRC522::PCD_CommunicateWithPICC (
    uint8_t command,
    uint8_t waitIRq,
    uint8_t * sendData,
    uint8_t sendLen,
    uint8_t * backData = NULL,
    uint8_t * backLen = NULL,
    uint8_t * validBits = NULL,
    uint8_t rxAlign = 0,
    bool checkCRC = false
)
```

Transfers data to the [**MFRC522**](mfrc522.md) FIFO, executes a commend, waits for completion and transfers data back from the FIFO. CRC validation can only be done if backData and backLen are specified.

**Parameters:**

* _command_ The command to execute. One of the PCD\_Command enums. 
* _waitIRq_ The bits in the ComIrqReg register that signals successful completion of the command. 
* _sendData_ Pointer to the data to transfer to the FIFO. 
* _sendLen_ Number of bytes to transfer to the FIFO. 
* _backData_ NULL or pointer to buffer if data should be read back after executing the command. 
* _backLen_ In: Max number of bytes to write to \*backData. Out: The number of bytes returned. 
* _validBits_ In/Out: The number of valid bits in the last byte. 0 for 8 valid bits. 
* _rxAlign_ In: Defines the bit position in backData\[0\] for the first bit received. Default 0. 
* _checkCRC_ In: True =&gt; The last two bytes of the response is assumed to be a CRC\_A that must be validated.

**Returns:**

STATUS\_OK on success, STATUS\_??? otherwise.

Transfers data to the [**MFRC522**](mfrc522.md) FIFO, executes a commend, waits for completion and transfers data back from the FIFO. CRC validation can only be done if backData and backLen are specified.

### function [PICC\_RequestA](mfrc522.md#1a3a93f92bf2b4c1fa6f3d76fd97a65190)

```cpp
uint8_t MFRC522::PICC_RequestA (
    uint8_t * bufferATQA,
    uint8_t * bufferSize
)
```

Transmits a REQuest command, Type A. Invites PICCs in state IDLE to go to READY and prepare for anticollision or selection. 7 bit frame. Beware: When two PICCs are in the field at the same time I often get STATUS\_TIMEOUT - probably due do bad antenna design.

**Parameters:**

* _bufferATQA_ The buffer to store the ATQA \(Answer to request\) in 
* _bufferSize_ Buffer size, at least two bytes. Also number of bytes returned if STATUS\_OK.

**Returns:**

STATUS\_OK on success, STATUS\_??? otherwise.

### function [PICC\_WakeupA](mfrc522.md#1a023b78fa99f1f0c8acd154584e3daa25)

```cpp
uint8_t MFRC522::PICC_WakeupA (
    uint8_t * bufferATQA,
    uint8_t * bufferSize
)
```

Transmits a Wake-UP command, Type A. Invites PICCs in state IDLE and HALT to go to READY\(\*\) and prepare for anticollision or selection. 7 bit frame. Beware: When two PICCs are in the field at the same time I often get STATUS\_TIMEOUT - probably due do bad antenna design.

**Parameters:**

* _bufferATQA_ The buffer to store the ATQA \(Answer to request\) in 
* _bufferSize_ Buffer size, at least two bytes. Also number of bytes returned if STATUS\_OK.

**Returns:**

STATUS\_OK on success, STATUS\_??? otherwise.

Transmits a Wake-UP command, Type A. Invites PICCs in state IDLE and HALT to go to READY\(\*\) and prepare for anticollision or selection. 7 bit frame. Beware: When two PICCs are in the field at the same time I often get STATUS\_TIMEOUT - probably due do bad antenna design.

### function [PICC\_REQA\_or\_WUPA](mfrc522.md#1a8b21b66da01172854c66def59fe9d07b)

```cpp
uint8_t MFRC522::PICC_REQA_or_WUPA (
    uint8_t command,
    uint8_t * bufferATQA,
    uint8_t * bufferSize
)
```

Transmits REQA or WUPA commands. Beware: When two PICCs are in the field at the same time I often get STATUS\_TIMEOUT - probably due do bad antenna design.

**Parameters:**

* _command_ The command to send - PICC\_CMD\_REQA or PICC\_CMD\_WUPA 
* _bufferATQA_ The buffer to store the ATQA \(Answer to request\) in 
* _bufferSize_ Buffer size, at least two bytes. Also number of bytes returned if STATUS\_OK.

**Returns:**

STATUS\_OK on success, STATUS\_??? otherwise.

### function [PICC\_Select](mfrc522.md#1a5d84996eaafe4ded4edca5bd4383c865)

```cpp
uint8_t MFRC522::PICC_Select (
    Uid * uid,
    uint8_t validBits = 0
)
```

Transmits SELECT/ANTICOLLISION commands to select a single PICC. Before calling this function the PICCs must be placed in the READY\(\*\) state by calling [**PICC\_RequestA\(\)**](mfrc522.md#1a3a93f92bf2b4c1fa6f3d76fd97a65190) or [**PICC\_WakeupA\(\)**](mfrc522.md#1a023b78fa99f1f0c8acd154584e3daa25). On success:

* The chosen PICC is in state ACTIVE\(\*\) and all other PICCs have returned to state IDLE/HALT. \(Figure 7 of the ISO/IEC 14443-3 draft.\)
* The UID size and value of the chosen PICC is returned in \*uid along with the SAK.

A PICC UID consists of 4, 7 or 10 bytes. Only 4 bytes can be specified in a SELECT command, so for the longer UIDs two or three iterations are used: UID size Number of UID bytes Cascade levels Example of PICC ======== =================== ============== =============== single 4 1 MIFARE Classic double 7 2 MIFARE Ultralight triple 10 3 Not currently in use?

**Parameters:**

* _uid_ Pointer to [**Uid**](https://github.com/ByzanceIoT/documentation-public/tree/3fe90b10188febdfcd320d169525b1b1c90c932e/hardware-a-programovani/programovani-hw/byzance-api/api/struct_m_f_r_c522_1_1_uid.md) struct. Normally output, but can also be used to supply a known UID. 
* _validBits_ The number of known UID bits supplied in \*uid. Normally 0. If set you must also supply uid-&gt;size.

**Returns:**

STATUS\_OK on success, STATUS\_??? otherwise.

### function [PICC\_HaltA](mfrc522.md#1ad5e79247f02c1abf4f7fb1ade26e6428)

```cpp
uint8_t MFRC522::PICC_HaltA (
    void 
)
```

Instructs a PICC in state ACTIVE\(\*\) to go to state HALT.

**Returns:**

STATUS\_OK on success, STATUS\_??? otherwise.

### function [PCD\_Authenticate](mfrc522.md#1a79f632aec9e2ca7c27fe4208f5d4843e)

```cpp
uint8_t MFRC522::PCD_Authenticate (
    uint8_t command,
    uint8_t blockAddr,
    MIFARE_Key * key,
    Uid * uid
)
```

Executes the [**MFRC522**](mfrc522.md) MFAuthent command. This command manages MIFARE authentication to enable a secure communication to any MIFARE Mini, MIFARE 1K and MIFARE 4K card. The authentication is described in the [**MFRC522**](mfrc522.md) datasheet section 10.3.1.9 and [http://www.nxp.com/documents/data\_sheet/MF1S503x.pdf](http://www.nxp.com/documents/data_sheet/MF1S503x.pdf) section 10.1. For use with MIFARE Classic PICCs. The PICC must be selected - ie in state ACTIVE\(\*\) - before calling this function. Remember to call [**PCD\_StopCrypto1\(\)**](mfrc522.md#1a087a46833537cab757014e5b01afe4f6) after communicating with the authenticated PICC - otherwise no new communications can start. All keys are set to FFFFFFFFFFFFh at chip delivery.

**Parameters:**

* _command_ PICC\_CMD\_MF\_AUTH\_KEY\_A or PICC\_CMD\_MF\_AUTH\_KEY\_B 
* _blockAddr_ The block number. See numbering in the comments in the .h file. 
* _key_ Pointer to the Crypteo1 key to use \(6 bytes\) 
* _uid_ Pointer to [**Uid**](https://github.com/ByzanceIoT/documentation-public/tree/3fe90b10188febdfcd320d169525b1b1c90c932e/hardware-a-programovani/programovani-hw/byzance-api/api/struct_m_f_r_c522_1_1_uid.md) struct. The first 4 bytes of the UID is used.

**Returns:**

STATUS\_OK on success, STATUS\_??? otherwise. Probably STATUS\_TIMEOUT if you supply the wrong key.

### function [PCD\_StopCrypto1](mfrc522.md#1a087a46833537cab757014e5b01afe4f6)

```cpp
void MFRC522::PCD_StopCrypto1 (
    void 
)
```

Used to exit the PCD from its authenticated state. Remember to call this function after communicating with an authenticated PICC - otherwise no new communications can start.

### function [MIFARE\_Read](mfrc522.md#1a2dbf95655f78503a119f30b3507cebcf)

```cpp
uint8_t MFRC522::MIFARE_Read (
    uint8_t blockAddr,
    uint8_t * buffer,
    uint8_t * bufferSize
)
```

Reads 16 bytes \(+ 2 bytes CRC\_A\) from the active PICC. For MIFARE Classic the sector containing the block must be authenticated before calling this function. For MIFARE Ultralight only addresses 00h to 0Fh are decoded. The MF0ICU1 returns a NAK for higher addresses. The MF0ICU1 responds to the READ command by sending 16 bytes starting from the page address defined by the command argument. For example; if blockAddr is 03h then pages 03h, 04h, 05h, 06h are returned. A roll-back is implemented: If blockAddr is 0Eh, then the contents of pages 0Eh, 0Fh, 00h and 01h are returned. The buffer must be at least 18 bytes because a CRC\_A is also returned. Checks the CRC\_A before returning STATUS\_OK.

**Parameters:**

* _blockAddr_ MIFARE Classic: The block \(0-0xff\) number. MIFARE Ultralight: The first page to return data from. 
* _buffer_ The buffer to store the data in 
* _bufferSize_ Buffer size, at least 18 bytes. Also number of bytes returned if STATUS\_OK.

**Returns:**

STATUS\_OK on success, STATUS\_??? otherwise.

### function [MIFARE\_Write](mfrc522.md#1a76c49a7d419120273586f145c53baec1)

```cpp
uint8_t MFRC522::MIFARE_Write (
    uint8_t blockAddr,
    uint8_t * buffer,
    uint8_t bufferSize
)
```

Writes 16 bytes to the active PICC. For MIFARE Classic the sector containing the block must be authenticated before calling this function. For MIFARE Ultralight the opretaion is called "COMPATIBILITY WRITE". Even though 16 bytes are transferred to the Ultralight PICC, only the least significant 4 bytes \(bytes 0 to 3\) are written to the specified address. It is recommended to set the remaining bytes 04h to 0Fh to all logic 0.

**Parameters:**

* _blockAddr_ MIFARE Classic: The block \(0-0xff\) number. MIFARE Ultralight: The page \(2-15\) to write to. 
* _buffer_ The 16 bytes to write to the PICC 
* _bufferSize_ Buffer size, must be at least 16 bytes. Exactly 16 bytes are written.

**Returns:**

STATUS\_OK on success, STATUS\_??? otherwise.

### function [MIFARE\_UltralightWrite](mfrc522.md#1a01800ec934813f6e89ef9ca3f05d20b2)

```cpp
uint8_t MFRC522::MIFARE_UltralightWrite (
    uint8_t page,
    uint8_t * buffer,
    uint8_t bufferSize
)
```

Writes a 4 byte page to the active MIFARE Ultralight PICC.

**Parameters:**

* _page_ The page \(2-15\) to write to. 
* _buffer_ The 4 bytes to write to the PICC 
* _bufferSize_ Buffer size, must be at least 4 bytes. Exactly 4 bytes are written.

**Returns:**

STATUS\_OK on success, STATUS\_??? otherwise.

### function [MIFARE\_Decrement](mfrc522.md#1ac779750e3f056d68aaa1b6a52ea757a9)

```cpp
uint8_t MFRC522::MIFARE_Decrement (
    uint8_t blockAddr,
    uint32_t delta
)
```

MIFARE Decrement subtracts the delta from the value of the addressed block, and stores the result in a volatile memory. For MIFARE Classic only. The sector containing the block must be authenticated before calling this function. Only for blocks in "value block" mode, ie with access bits \[C1 C2 C3\] = \[110\] or \[001\]. Use [**MIFARE\_Transfer\(\)**](mfrc522.md#1a44aaaf9a3310fc1c67daddf8733f579b) to store the result in a block.

**Parameters:**

* _blockAddr_ The block \(0-0xff\) number. 
* _delta_ This number is subtracted from the value of block blockAddr.

**Returns:**

STATUS\_OK on success, STATUS\_??? otherwise.

### function [MIFARE\_Increment](mfrc522.md#1ad2ff3ec8a7c323a86a4f9769f1bf564f)

```cpp
uint8_t MFRC522::MIFARE_Increment (
    uint8_t blockAddr,
    uint32_t delta
)
```

MIFARE Increment adds the delta to the value of the addressed block, and stores the result in a volatile memory. For MIFARE Classic only. The sector containing the block must be authenticated before calling this function. Only for blocks in "value block" mode, ie with access bits \[C1 C2 C3\] = \[110\] or \[001\]. Use [**MIFARE\_Transfer\(\)**](mfrc522.md#1a44aaaf9a3310fc1c67daddf8733f579b) to store the result in a block.

**Parameters:**

* _blockAddr_ The block \(0-0xff\) number. 
* _delta_ This number is added to the value of block blockAddr.

**Returns:**

STATUS\_OK on success, STATUS\_??? otherwise.

### function [MIFARE\_Restore](mfrc522.md#1a26cd9238e46b35e8adcb68acb2127f77)

```cpp
uint8_t MFRC522::MIFARE_Restore (
    uint8_t blockAddr
)
```

MIFARE Restore copies the value of the addressed block into a volatile memory. For MIFARE Classic only. The sector containing the block must be authenticated before calling this function. Only for blocks in "value block" mode, ie with access bits \[C1 C2 C3\] = \[110\] or \[001\]. Use [**MIFARE\_Transfer\(\)**](mfrc522.md#1a44aaaf9a3310fc1c67daddf8733f579b) to store the result in a block.

**Parameters:**

* _blockAddr_ The block \(0-0xff\) number.

**Returns:**

STATUS\_OK on success, STATUS\_??? otherwise.

MIFARE Restore copies the value of the addressed block into a volatile memory.

### function [MIFARE\_Transfer](mfrc522.md#1a44aaaf9a3310fc1c67daddf8733f579b)

```cpp
uint8_t MFRC522::MIFARE_Transfer (
    uint8_t blockAddr
)
```

MIFARE Transfer writes the value stored in the volatile memory into one MIFARE Classic block. For MIFARE Classic only. The sector containing the block must be authenticated before calling this function. Only for blocks in "value block" mode, ie with access bits \[C1 C2 C3\] = \[110\] or \[001\].

**Parameters:**

* _blockAddr_ The block \(0-0xff\) number.

**Returns:**

STATUS\_OK on success, STATUS\_??? otherwise.

### function [PCD\_MIFARE\_Transceive](mfrc522.md#1a6d42d0615c3e956278658cddb487ba09)

```cpp
uint8_t MFRC522::PCD_MIFARE_Transceive (
    uint8_t * sendData,
    uint8_t sendLen,
    bool acceptTimeout = false
)
```

Wrapper for MIFARE protocol communication. Adds CRC\_A, executes the Transceive command and checks that the response is MF\_ACK or a timeout.

**Parameters:**

* _sendData_ Pointer to the data to transfer to the FIFO. Do NOT include the CRC\_A. 
* _sendLen_ Number of bytes in sendData. 
* _acceptTimeout_ True =&gt; A timeout is also success

**Returns:**

STATUS\_OK on success, STATUS\_??? otherwise.

### function [PICC\_GetType](mfrc522.md#1a827930d1a50d63402d7edcda5a74093d)

```cpp
uint8_t MFRC522::PICC_GetType (
    uint8_t sak
)
```

Translates the SAK \(Select Acknowledge\) to a PICC type.

**Parameters:**

* _sak_ The SAK byte returned from [**PICC\_Select\(\)**](mfrc522.md#1a5d84996eaafe4ded4edca5bd4383c865).

**Returns:**

PICC\_Type

### function [PICC\_GetTypeName](mfrc522.md#1ac3b1289ba9a0f0dd4b117071c52a1764)

```cpp
char * MFRC522::PICC_GetTypeName (
    uint8_t type
)
```

Returns a string pointer to the PICC type name.

**Parameters:**

* _type_ One of the PICC\_Type enums.

**Returns:**

A string pointer to the PICC type name.

### function [GetStatusCodeName](mfrc522.md#1a4469297fa43eca37db6505ad2922c0f3)

```cpp
char * MFRC522::GetStatusCodeName (
    uint8_t code
)
```

Returns a string pointer to a status code name.

**Parameters:**

* _code_ One of the StatusCode enums.

**Returns:**

A string pointer to a status code name.

### function [MIFARE\_SetAccessBits](mfrc522.md#1ac82a4d75dd70d25afbd24726e91796b3)

```cpp
void MFRC522::MIFARE_SetAccessBits (
    uint8_t * accessBitBuffer,
    uint8_t g0,
    uint8_t g1,
    uint8_t g2,
    uint8_t g3
)
```

Calculates the bit pattern needed for the specified access bits. In the \[C1 C2 C3\] tupples C1 is MSB \(=4\) and C3 is LSB \(=1\).

**Parameters:**

* _accessBitBuffer_ Pointer to byte 6, 7 and 8 in the sector trailer. Bytes \[0..2\] will be set. 
* _g0_ Access bits \[C1 C2 C3\] for block 0 \(for sectors 0-31\) or blocks 0-4 \(for sectors 32-39\) 
* _g1_ Access bits \[C1 C2 C3\] for block 1 \(for sectors 0-31\) or blocks 5-9 \(for sectors 32-39\) 
* _g2_ Access bits \[C1 C2 C3\] for block 2 \(for sectors 0-31\) or blocks 10-14 \(for sectors 32-39\) 
* _g3_ Access bits \[C1 C2 C3\] for the sector trailer, block 3 \(for sectors 0-31\) or block 15 \(for sectors 32-39\) 

### function [PICC\_IsNewCardPresent](mfrc522.md#1a2bd3bd7586a52fa107e0e71c7f073eb2)

```cpp
bool MFRC522::PICC_IsNewCardPresent (
    void 
)
```

Returns true if a PICC responds to PICC\_CMD\_REQA. Only "new" cards in state IDLE are invited. Sleeping cards in state HALT are ignored.

**Returns:**

bool

### function [PICC\_ReadCardSerial](mfrc522.md#1a3664b1b301d6e740bdab01842622670e)

```cpp
bool MFRC522::PICC_ReadCardSerial (
    void 
)
```

Simple wrapper around PICC\_Select. Returns true if a UID could be read. Remember to call [**PICC\_IsNewCardPresent\(\)**](mfrc522.md#1a2bd3bd7586a52fa107e0e71c7f073eb2), [**PICC\_RequestA\(\)**](mfrc522.md#1a3a93f92bf2b4c1fa6f3d76fd97a65190) or [**PICC\_WakeupA\(\)**](mfrc522.md#1a023b78fa99f1f0c8acd154584e3daa25) first. The read UID is available in the class variable uid.

**Returns:**

bool

The documentation for this class was generated from the following file: `D:/w/hw-libs/\_libs\_/libraries/MFRC522.h`

