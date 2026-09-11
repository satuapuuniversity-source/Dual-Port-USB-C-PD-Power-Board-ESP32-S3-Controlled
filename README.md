# DualPort USB-C PD Power Board (ESP32-S3 Controlled)

A dual-port USB-C Power Delivery source board with LiPo battery backup (UPS-style operation), controlled by an ESP32-S3. This design evolved from an earlier router UPS/power-management board (BQ25703A + MT3608) into a full dual-channel USB-C PD output system.

## Hardware

### MCU & Control
- **ESP32-S3-WROOM-1-N8R8** - main controller (monitors current/voltage, manages charging and PD output enable/disable)
- **2N7002** - power-path MOSFET
- Push-button + status LED

### Battery / Charging (LiPo Battery Charger IC + DW01A sheets)
- **BQ25703ARSNR** - buck-boost battery charger IC
- **5x CSD17579Q3A** - power MOSFETs (charge path, output switching)
- **BQ7692000PWR** - battery protection IC
- **DW01A** - secondary battery protection
- **MT3608** - boost converter (12V rail generation)
- **AO3401A** - P-MOSFET
- **NTCG103JF103FT1** - NTC thermistor (thermal monitoring)
- **SMBJ15A** - TVS surge protection
- **MF-MSMF250** - resettable PTC fuses
- **B2B-PH-K-S** - JST battery connector

### Current/Voltage Sensing
- **2x INA219AIDCNR** - current/voltage sense, one per output port
- **AP2112K-3.3** - 3.3V LDO for sense circuitry
- Precision R010 (0.01Ω) current-sense resistors (CRA2512-FZ-R010ELF)

### USB-C Input / PD Negotiation
- **STUSB4500QTR** - USB-C PD sink controller (negotiates input power)
- **GT-USB-7010B** - USB-C connector
- **PRTR5V0U2X** - ESD protection array
- **SMBJ5.0A** - TVS diode

### USB-C PD Outputs (usb out1 / usb out2) - 2 identical independent channels
Each output channel includes:
- **TPS25740RGER** - USB-C PD source controller
- **TPS55289RYQR** - buck-boost converter (adjustable PD output voltage)
- **CSD17579Q3A** - power MOSFET
- **USB_C_Receptacle_USB2.0_16P** - USB-C output connector
- MF-MSMF250 resettable fuse, status LED
- (usb out2 additionally includes a **TXS0102DCUR** level-shifter)

## Repo structure
- `*.kicad_sch` (main, INA219, LiPo Battery Charger IC, DW01A, USB, usb out1, usb out2, untitled) / `.kicad_pcb` / `.kicad_pro` / `.kicad_prl` - KiCad project files
- `Bills of materials/` - BOM (CSV)
- `Component placement file/` - pick-and-place position file
- `Garber file/` - manufacturing gerbers + PTH/NPTH drill files + job file

**Scope:** hardware/PCB design only - firmware (ESP32-S3 monitoring/control logic) not included in this repo.
