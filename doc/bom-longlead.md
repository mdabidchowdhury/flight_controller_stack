# Long-Lead & High-Risk Bill of Materials (BOM) Audit

## Active Supply Risk Checklist (Design-Only Verification)
| Component | MPN / Class | Role / Board | Risk Factor & Selection Rationale | Lifecycle / Stock Status |
| :--- | :--- | :--- | :--- | :--- |
| **Flight MCU** | `STM32H743VIT6` | FC Flight Controller | LQFP-100 package required for hand-reworkability and probing[cite: 2]. High pin-count flagship target for INAV 7+[cite: 2]. | Active / Verify Stock |
| **Co-Processor** | `ESP32-S3-WROOM-1-N8R8` | FC Wireless Bridge | 8 MB Flash / 8 MB PSRAM module[cite: 2]. Do not use bare die (avoids RF certification and antenna tuning)[cite: 2]. | Active / Verify Stock |
| **IMU Sensor** | `ICM-42688-P` | FC Motion Tracking | Replaces EOL MPU-6000[cite: 2]. Must check stock as gyro sensor availability fluctuates. | Active / Verify Stock |
| **Barometer** | `DPS310` | FC Altitude | High-precision (~5 cm) pressure sensor required for INAV navigation and RTH[cite: 2]. | Active / Verify Stock |
| **Blackbox Flash** | `W25Q128JVSIQ` | FC Data Logging | 16 MB NOR Flash on dedicated SPI2 bus[cite: 2]. Avoids bus contention with the 8 kHz gyro[cite: 2]. | Active / Verify Stock |
| **OSD Chip** | `AT7456E` | FC Video Overlay | Analog video character generator[cite: 2]. Populate on analog SKU only (`DNP_variant`)[cite: 2]. | Active / Verify Stock |
| **ESC MCUs (×4)**| `STM32G071KBU6` | ESC Channel Control | One MCU per motor running AM32 firmware[cite: 2]. Replaces closed-source BLHeli_32 silicon[cite: 2]. | Active / Verify Stock |
| **Gate Drivers (×4)**| `FD6288Q` / `MP6531` | ESC Half-Bridge Driver | Integrated 3-phase driver with internal bootstrap diodes and shoot-through protection[cite: 2]. | Active / Verify Stock |
| **MOSFETs (×24)**| `ISC030N04NM6` class | ESC Power Stage | 40 V N-channel PQFN 5×6 mm, $R_{DS(on)} \le 1.6\text{ m}\Omega$, $Q_g < 40\text{ nC}$[cite: 2]. **Must be rated $\ge 40\text{ V}$ for 6S**[cite: 2]. | Active / Verify Stock |
| **Current Sense Amp**| `INA240` | ESC Telemetry | Enhanced PWM rejection specifically designed for motor switching environments[cite: 2]. | Active / Verify Stock |
| **Step-Down Bucks**| `MP4560` / `TPS54331`| FC 9V & 5V Rails | High-voltage step-down converters[cite: 2]. Must tolerate $\ge 35\text{ V}$ to survive regenerative braking spikes[cite: 2]. | Active / Verify Stock |
| **Low-Noise LDOs** | `TLV75533` / `TLV75733`| FC 3.3V Rails | Two separate LDOs required to isolate noisy ESP32-S3 Wi-Fi bursts from sensitive MCU/IMU sensors[cite: 2]. | Active / Verify Stock |
| **Bulk Polymer Caps**| $220\mu\text{F}$ 35V Polymer | ESC Onboard Filter | $\ge 4$ solid polymer capacitors distributed across FET banks to absorb voltage transients[cite: 2]. | Active / Verify Stock |