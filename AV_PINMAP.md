# Aerolotl AV: STM32G473VET6 pin map

The H723 was swapped for an STM32G474VETx, which is also LQFP-100 and uses the same footprint. On 2026-10-06 the part became the STM32G473VET6: the same chip without HRTIM (unused here), with the same pinout and better stock. The schematic still uses the STM32G474VETx symbol for the pin alternates.
Signals were kept on the same side of the chip wherever an alternate function allowed it, so the existing placement still works.

Validate this in STM32CubeMX before you write firmware.

| Pin | Port | Function | Net | Was H723 pin |
|---|---|---|---|---|
| 1 | PE2 | GPIO | `/External/GPIO.PE2` | 1 |
| 2 | PE3 | GPIO | `/External/GPIO.PE3` | 2 |
| 3 | PE4 | GPIO | `/External/GPIO.PE4` | 3 |
| 4 | PE5 | GPIO | `/External/GPIO.PE5` | 4 |
| 5 | PE6 | GPIO | `/External/GPIO.PE6` | 5 |
| 6 | VBAT | power | `+3V3` | 6 |
| 8 | PC14 | LSE OSC32_IN | `/MCU/LS_OSC_A` | 8 |
| 9 | PC15 | LSE OSC32_OUT | `/MCU/LS_OSC_B` | 9 |
| 12 | PF0 | HSE OSC_IN | `/MCU/HS_OSC_A` | 12 |
| 13 | PF1 | HSE OSC_OUT | `/MCU/HS_OSC_B` | 13 |
| 14 | PG10/NRST | NRST | `/Debugger/T_NRST` | 14 |
| 15 | PC0 | ADC1_IN6 | `/Power/VOLT_SENSE` (VBAT x 22k/32k) | 15 |
| 7 | PC13 | EXTI13 | `RADIO_DIO3` (LoRa) | - |
| 11 | PF10 | EXTI10 | `RADIO_DIO1` (LoRa) | - |
| 16 | PC1 | GPIO in | `/MCU/PWR_STS` | 16 |
| 17 | PC2 | GPIO in | `RADIO_DIO2` (LoRa) | - |
| 18 | PC3 | EXTI3 | `RADIO_DIO0` (LoRa) | - |
| 19 | PF2 | GPIO in | `RADIO_DIO4` (LoRa) | - |
| 20 | PA0 | ADC1_IN1 | `/Igniter/SENSE_I0` | 22 |
| 21 | PA1 | ADC1_IN2 | `/Igniter/SENSE_I1` | 23 |
| 22 | PA2 | USART2_TX | `/Sensors/M10S.RX` | 24 |
| 23 | VSS | power | `GND` | 10 |
| 24 | VDD | power | `+3V3` | 11 |
| 25 | PA3 | USART2_RX | `/Sensors/M10S.TX` | 25 |
| 26 | PA4 | - | no-connect (was SPARE_ADC1) | 28 |
| 27 | PA5 | SPI1_SCK | `/MCU/SPI1.SCK` | 29 |
| 28 | PA6 | SPI1_MISO | `/MCU/SPI1.MISO` | 30 |
| 29 | PA7 | SPI1_MOSI | `/MCU/SPI1.MOSI` | 31 |
| 30 | PC4 | GPIO | `/Indicators/LED.R` | 32 |
| 31 | PC5 | GPIO | `/Indicators/LED.G` | 33 |
| 32 | PB0 | EXTI0 | `/MCU/SPI1.INT_345` | 64 |
| 33 | PB1 | EXTI1 | `/MCU/SPI1.INT_BMP` | 96 |
| 34 | PB2 | EXTI2 | `/MCU/SPI1.INT_IMU_GYRO` | 36 |
| 35 | VSSA | power | `GND` | 19 |
| 36 | VREF+ | power | `/MCU/VREFP` | 20 |
| 37 | VDDA | power | `+3.3VA` | 21 |
| 38 | PE7 | GPIO | `/External/GPIO.PE7` | 37 |
| 39 | PE8 | GPIO | `/External/GPIO.PE8` | 38 |
| 40 | PE9 | GPIO | `/External/GPIO.PE9` | 39 |
| 41 | PE10 | GPIO | `/External/GPIO.PE10` | 40 |
| 42 | PE11 | GPIO | `/External/GPIO.PE11` | 41 |
| 43 | PE12 | SPI4_SCK | `/External/SPI4.SCK` (LoRa only) | 42 |
| 44 | PE13 | SPI4_MISO | `/External/SPI4.MISO` | 43 |
| 45 | PE14 | SPI4_MOSI | `/External/SPI4.MOSI` | 44 |
| 46 | PE15 | EXTI15 | `/MCU/SPI1.INT_IMU_ACC` | 45 |
| 47 | PB10 | LPUART1_RX | `/External/LPUART1_TARGET_RX` | 97 |
| 48 | VSS | power | `GND` | 26 |
| 49 | VDD | power | `+3V3` | 27 |
| 50 | PB11 | LPUART1_TX | `/External/LPUART1_TARGET_TX` | 98 |
| 51 | PB12 | SPI2 CS (GPIO) | `/MCU/SPI2.CS` | 51 |
| 52 | PB13 | SPI2_SCK | `/MCU/SPI2.SCK` | 52 |
| 53 | PB14 | SPI2_MISO | `/MCU/SPI2.MISO` | 53 |
| 54 | PB15 | SPI2_MOSI | `/MCU/SPI2.MOSI` | 54 |
| 55 | PD8 | USART3_TX | `/External/USART3_TARGET_TX` | 55 |
| 56 | PD9 | USART3_RX | `/External/USART3_TARGET_RX` | 56 |
| 57 | PD10 | GPIO in | `/MCU/SPI2.BUSY` | 57 |
| 58 | PD11 | GPIO out | `/MCU/SPI2.RST` | 58 |
| 59 | PD12 | TIM4_CH1 | `/Indicators/LED.B` | 63 |
| 60 | PD13 | TIM4_CH2 | `/Indicators/LED` | 77 |
| 61 | PD14 | GPIO out | `/Igniter/IGN0` | 61 |
| 62 | PD15 | GPIO out | `/Igniter/IGN1` | 62 |
| 63 | VSS | power | `GND` | 49 |
| 64 | VDD | power | `+3V3` | 50 |
| 65 | PC6 | I2C4_SCL | `/External/I2C4.SCL` | 59 |
| 66 | PC7 | I2C4_SDA | `/External/I2C4.SDA` | 60 |
| 67 | PC8 | I2C3_SCL | `/External/I2C3.SCL` | 46 |
| 68 | PC9 | I2C3_SDA | `/External/I2C3.SDA` | 47 |
| 69 | PA8 | TIM1_CH1 (PWM) | `/Indicators/BUZZER` | 67 |
| 70 | PA9 | USART1_TX | `/Debugger/T_VCP_RX` | 68 |
| 71 | PA10 | USART1_RX | `/Debugger/T_VCP_TX` | 69 |
| 72 | PA11 | USB_DM | `/MCU/USB_D-` | 70 |
| 73 | PA12 | USB_DP | `/MCU/USB_D+` | 71 |
| 74 | VSS | power | `GND` | 74 |
| 75 | VDD | power | `+3V3` | 75 |
| 76 | PA13 | SWDIO | `/Debugger/T_SWDIO` | 72 |
| 77 | PA14 | SWCLK | `/Debugger/T_SWCLK` | 76 |
| 78 | PA15 | I2C1_SCL | `/External/I2C1.SCL` | 92 |
| 79 | PC10 | SPI3_SCK | `/MCU/SDSPI.SCK` | 80 |
| 80 | PC11 | SPI3_MISO | `/MCU/SDSPI.MISO` | 65 |
| 81 | PC12 | SPI3_MOSI | `/MCU/SDSPI.MOSI` | 83 |
| 82 | PD0 | SPI3 CS (GPIO) | `/MCU/SDSPI.CS` | 79 |
| 83 | PD1 | GPIO out | `RADIO_NSS` (LoRa CS, 10k pull-up) | - |
| 84 | PD2 | GPIO out (open-drain) | `RADIO_RST` (LoRa) | - |
| 85 | PD3 | GPIO | `/MCU/SPI1.CS_IMU_ACC` | 84 |
| 86 | PD4 | GPIO | `/MCU/SPI1.CS_IMU_GYRO` | 85 |
| 87 | PD5 | GPIO | `/MCU/SPI1.CS_BMP` | 86 |
| 88 | PD6 | GPIO | `/MCU/SPI1.CS_345` | 87 |
| 89 | PD7 | GPIO | `/MCU/SPI1.CS_375` | 88 |
| 90 | PB3 | SWO | `/Debugger/T_SWO` | 89 |
| 91 | PB4 | GPIO out | `/MCU/GPS_RST` | 91 |
| 94 | PB7 | I2C1_SDA | `/External/I2C1.SDA` | 93 |
| 95 | PB8/BOOT0 | BOOT0 | `/MCU/BOOT0` | 94 |
| 96 | PB9 | EXTI9 | `/MCU/SPI1.INT_375` | 95 |
| 99 | VSS | power | `GND` | 99 |
| 100 | VDD | power | `+3V3` | 100 |

**Free pins:** PF9, PA4, PB5, PB6, PE0, PE1. They are flagged NC in the schematic.

- **PB5/PB6 are reserved for FDCAN2** (RX/TX) for a future AV↔AB CAN link.
- **LoRa radio (U10, Ra-01H / SX1276)** has SPI4 to itself (J5 header removed). Only DIO0/DIO1/DIO3 have interrupt lines; DIO2/DIO4 are polled. Keep PD1 high and put the radio to sleep (or hold PD2 low) when unused. Drive PD2 open-drain. Never transmit without an antenna or 50R load on J4. IREC SRAD band: 913.0-917.0 MHz, <=500 mW, no hopping.

## Firmware notes

- **SD card is now SPI mode on SPI3,** because the G4 has no SDMMC. CS is PD0 (GPIO). The card-side DAT1/DAT2 pull-ups stay populated.
- **The interrupt pins use separate EXTI lines** (0, 1, 2, 9, 15), so they never share an interrupt.
- **Clocks:**
  - SYSCLK 170 MHz = 25 MHz HSE / 5 × 68 / 2.
  - Take USB 48 MHz from HSI48 + CRS (SOF sync), because 48 MHz is not reachable from that PLL.
- **BOOT0 is on PB8.** Keep option bit nSWBOOT0 = 1 (the default) so the BOOT0 pin + SW and pull-down still work.
- **There are no VCAP pins on the G4,** so C67/C68 (2.2 µF) were deleted.
- **Renamed nets:** I2C2 → I2C3 (Stemma CN2), UART8 → LPUART1 (J10 header), SDMMC1.* → SDSPI.*.
- **Battery (1S, since 2026-10-06):** VBAT = V(PC0) × 1.4545. 4.2 V full reads 2.89 V, 3.0 V empty reads 2.06 V.
- **Igniter sense (PA0/PA1):** open ≈ 1.0 V, e-match present ≈ 0 V, firing ≈ 2.9 V.
- **PWR_STS (PC1)** is low while the TPS2116 runs from the battery (VIN2) and high on USB.
