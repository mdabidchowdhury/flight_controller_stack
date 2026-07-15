# Inter-Board Interface Contract (8-Pin Ribbon)

## Physical Specification
* **Connector Type:** 8-pin JST-SH 1.0 mm pitch.
* **Stack Order:** ESC on the bottom (battery side), FC on top. This orientation keeps high-current 200 A paths and their interfering magnetic fields away from the flight controller's gyro.

## Pin Assignment & Electrical Contract
| Pin | Name | Direction | Voltage Level / Protocol | Notes |
| :--- | :--- | :--- | :--- | :--- |
| **1** | `VBAT` | ESC → FC | 9 V – 25.2 V (3–6S LiPo) | Main battery feed to FC 9V/5V bucks and VBAT ADC divider. |
| **2** | `GND` | Shared | 0 V Reference | Common ground reference between FC and ESC. |
| **3** | `CURR` | ESC → FC | Analog, 0 – 3.3 V Full-Scale | Scaled current sense from ESC INA240 amp, routed to H743 pin PC1. Print A/V scale on silk. |
| **4** | `TLM` | ESC → FC | Open-Drain / AM32 Telemetry | Routed to H743 UART7 RX (PE7). Must have exactly one 4.7 kΩ pull-up to 3.3 V on the FC side. |
| **5** | `M1` | FC → ESC | 3.3 V DShot300/600 | Motor 1 command from H743 TIM3 CH1. |
| **6** | `M2` | FC → ESC | 3.3 V DShot300/600 | Motor 2 command from H743 TIM3 CH2. |
| **7** | `M3` | FC → ESC | 3.3 V DShot300/600 | Motor 3 command from H743 TIM3 CH3. |
| **8** | `M4` | FC → ESC | 3.3 V DShot300/600 | Motor 4 command from H743 TIM3 CH4. |

## Critical Design Rules 
* **3D Connector Mirroring:** Before ordering, both boards must be exported as STEP files from KiCad 9 and assembled in a 3D viewer to physically verify that pin 1 mates with pin 1 through the ribbon. Mirrored headers are a common mechanical failure.
* **Motor Numbering Silk:** Motor numbers must be explicitly printed on both silkscreens. INAV's default quad-X motor order differs from Betaflight's; the INAV convention must be clearly stated on the silk to prevent accidental flipping on arming.
* **TLM Pull-Up Isolation:** Do not place pull-up resistors on the ESC side. Placing a single 4.7 kΩ pull-up on the FC side ensures the resistor exists exactly once and terminates the transmission line properly without overloading the G071 open-drain outputs.