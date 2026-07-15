# STM32H743VIT6 (LQFP-100) Pinout & Peripheral Allocation

## VCAP & Core Power (Boot-Critical)
| Function | Pin Number (LQFP-100) | Net / Requirement | Notes |
| :--- | :--- | :--- | :--- |
| **VCAP1** | Pin 48 | `VCAP1` | Requires dedicated 2.2 µF low-ESR ceramic to GND |
| **VCAP2** | Pin 73 | `VCAP2` | Requires dedicated 2.2 µF low-ESR ceramic to GND (Do NOT share with VCAP1) |

## Peripheral Allocation Table
| Function | Peripheral | Pins | Notes |
| :--- | :--- | :--- | :--- |
| **IMU (ICM-42688-P)** | SPI1 | SCK: PA5, MISO: PA6, MOSI: PA7<br>CS: PC4 | INT1 → PC5 (EXTI) |
| **Blackbox (W25Q128)** | SPI2 | SCK: PB13, MISO: PB14, MOSI: PB15<br>CS: PB12 | 16 MB NOR Flash |
| **OSD (AT7456E)** | SPI3 | SCK: PC10, MISO: PC11, MOSI: PC12<br>CS: PA15 | Populate on analog SKU only (DNP variant) |
| **Barometer & Ext. Compass** | I2C1 | SCL: PB8, SDA: PB9 | DPS310 baro onboard; compass via GPS pad group. Add 2.2 kΩ pull-ups |
| **ESP32-S3 Link (MSP)** | USART1 | TX: PA9, RX: PA10 | Cross-connected to S3 U1RXD / U1TXD. S3 EN → PE3 |
| **GPS** | USART2 | TX: PD5, RX: PD6 | 5V + I2C1 brought out on pad group |
| **RC Receiver (CRSF)** | USART3 | TX: PD8, RX: PD9 | 4-pin JST-SH bay |
| **VTX (MSP DisplayPort)** | USART6 | TX: PC6, RX: PC7 | Or SmartAudio on TX |
| **ESC Telemetry** | UART7 | RX: PE7 | RX only. Connected to TLM ribbon pin. 4.7 kΩ pull-up on FC side |
| **Spare / Debug** | UART8 | TX: PE0, RX: PE1 | Solder pads |
| **Motors M1 – M4** | TIM3 | CH1: PB4, CH2: PB5<br>CH3: PB0, CH4: PB1 | All 4 motors on ONE timer for burst DMA |
| **VBAT Sense** | ADC1 | PC0 | 10k:1k divider, 1 kΩ series + BAT54S clamp + 100 nF to GND |
| **Current Sense** | ADC1 | PC1 | From ESC CURR ribbon pin. 1 kΩ series + BAT54S clamp |
| **Buzzer** | GPIO | PD15 | AO3400 low-side MOSFET + diode |
| **WS2812 LED** | TIM4 | CH1: PD12 | DMA-capable timer pin |
| **SWD Debug** | SWD | SWDIO: PA13, SWCLK: PA14 | On 5-pad group / 1.27 mm header with NRST, 3V3, GND |
| **USB PHY** | USB_OTG_FS | D-: PA11, D+: PA12 | Route as 90 Ω differential pair. Independent 5.1 kΩ pull-downs on CC1/CC2 |