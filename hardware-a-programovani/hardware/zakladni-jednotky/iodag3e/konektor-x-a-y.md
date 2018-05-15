# Konektor X a Y

Podrobný popis konektorů X a Y včetně všech periferií \(sběrnice UART, I2C, SPI, CAN, dále pak časovač TIM, dostupnost ADC a DAC\). Umístění a pinout kounektorů viz. [GPIO a sběrnice](https://docu.byzance.cz/hardware-a-programovani/hardware/zakladni-jednotky/iodag3e/rozhrani-a-periferie#gpio-a-sbernice).

## Konektor X

| X | MCU | UART | I2C | SPI | CAN | TIM | ADC | DAC |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| X00 | PB1 |  |  |  |  |  ✓ | ADC12\_IN8 |  |
| X01 | PB0 |  |  |  |  |  ✓ | ADC12\_IN9 |  |
| X02 | PE9 |  |  |  |  |  ✓ |  |  |
| X03 | PB2 |  |  |  |  |  |  |  |
| X04 | PA3 | USART2\_RX |  |  |  |  ✓ | ADC123\_IN3 |  |
| X05 | PA6 |  |  | SPI1\_MISO |  |  ✓ | ADC12\_IN6 |  |
| X06 | PB6 | USART1\_TX | I2C1\_SCL |  | CAN2\_TX |  ✓ |  |  |
| X07 | PB7 | USART1\_RX | I2C1\_SDA |  |  |  |  |  |
| X08 | PA15 |  |  |  |  |  |  |  |
| X09 | PD9 | USART3\_RX |  |  |  |  |  |  |
| X10 | PB3 |  |  |  |  |  |  |  |
| X11 | PD8 | USART3\_TX |  |  |  |  |  |  |
| X12 | PB4 |  |  |  |  |  |  |  |
| X13 | PB9 |  |  |  |  |  ✓ |  |  |
| X14 | PB5 |  |  |  |  |  ✓ |  |  |
| X15 | PB8 |  |  |  |  |  ✓ |  |  |

## Konektor Y

| Y | MCU | UART | I2C | SPI | CAN | TIM | ADC | DAC |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Y00 | PC10 | UART3/4\_TX |  | SPI3\_SCK |  |  |  |  |
| Y01 | PC11 | UART3/4\_RX |  | SPI3\_MISO |  |  |  |  |
| Y02 | PD0 |  |  |  | CAN1\_RX |  |  |  |
| Y03 | PC12 | UART5\_TX |  | SPI3\_MOSI |  |  |  |  |
| Y04 | PD1 |  |  |  | CAN1\_TX |  |  |  |
| Y05 | PI0 |  |  |  |  |  ✓ |  |  |
| Y06 | PC9 |  | I2C3\_SDA |  |  |  ✓ |  |  |
| Y07 | PA8 |  | I2C3\_SCL |  |  |  ✓ |  |  |
| Y08 | PC8 | USART6\_CK |  |  |  |  ✓ |  |  |
| Y09 | PC7 | USART6\_RX |  |  |  |  ✓ |  |  |
| Y10 | PC6 | USART6\_TX |  |  |  |  ✓ |  |  |
| Y11 | PG8 | USART6\_RTS |  | SPI6\_NSS |  |  |  |  |
| Y12 | PH12 |  |  |  |  |  ✓ |  |  |
| Y13 | PH11 |  |  |  |  |  ✓ |  |  |
| Y14 | PH10 |  |  |  |  |  ✓ |  |  |
| Y15 | PG13 | USART6\_CTS |  | SPI6\_CLK |  |  |  |  |
| Y16 | PG14 | USART6\_TX |  | SPI6\_MOSI |  |  |  |  |
| Y17 | PG12 | USART6\_RTS |  | SPI6\_MISO |  |  |  |  |
| Y18 | PD2 | UART5\_RX |  |  |  |  ✓ |  |   |
| Y19 | PC0 |  |  |  |  |  | ADC123\_IN10 |  |
| Y20 | PH8 |  | I2C3\_SDA |  |  |  |  |  |
| Y21 | PH7 |  | I2C3\_SCL |  |  |  |  |  |
| Y22 | PC3 |  |  |  |  |  | ADC123\_IN13 |  |
| Y23 | PA4 |  |  | SPI3\_NSS |  |  | ADC12\_IN4 |  ✓ |
| Y24 | PC2 |  |  |  |  |  | ADC123\_IN12 |  ✓ |
| Y25 | PA5 |  |  | SPI1\_SCK |  |  ✓ | ADC12\_IN5 |  |
| Y26 | PB10 | USART3\_TX |  |  |  |  ✓ |  |  |

