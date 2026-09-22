<div align="center">

# 🚁 ESP32 Drone Controller Board

**A Wi-Fi/Bluetooth micro-drone where the PCB *is* the airframe. Flight controller, motor drivers, sensors, and LiPo charging all sit on one 2-layer board.**

![KiCad](https://img.shields.io/badge/KiCad-10-314CB0?logo=kicad&logoColor=white)
![MCU](https://img.shields.io/badge/MCU-ESP32--WROOM--32E-E7352C?logo=espressif&logoColor=white)
![Layers](https://img.shields.io/badge/PCB-2--layer%20%7C%201.6mm-2E7D32)
![Fab](https://img.shields.io/badge/Fab-JLCPCB%20ready-F57C00)

<img src="%D7%AA%D7%9E%D7%95%D7%A0%D7%95%D7%AA/3D_Hero.png" width="560" alt="3D render of the drone board">

</div>

---

## ✨ Highlights

- **PCB airframe:** four arms with integrated motor mounts and landing legs, ~103 × 104 mm, so no separate frame is needed.
- **ESP32-WROOM-32E** with an on-board antenna keep-out, for Wi-Fi / BLE control.
- **Four brushed-motor channels:** logic-level MOSFETs with flyback diodes and gate resistors on every channel.
- **Flight sensors:** a 6-axis IMU and a barometric pressure sensor for altitude hold.
- **USB-C:** programming through a USB-UART bridge with auto-reset, plus single-cell LiPo charging.
- **Manufacturing ready:** Gerbers, drill files, BOM, and CPL with JLCPCB part numbers.

## 🧩 Block Diagram

```mermaid
flowchart LR
    USB[USB-C] --> UART[CH340K<br/>USB-UART]
    USB --> CHG[TP4056<br/>LiPo Charger]
    CHG --> BAT[(1S LiPo)]
    BAT --> LDO[AP2112K<br/>3.3V LDO]
    LDO --> MCU[ESP32-WROOM-32E]
    UART -- auto-reset --> MCU
    MCU -- I2C --> IMU[LSM6DS3<br/>6-axis IMU]
    MCU -- I2C --> BARO[LPS22HB<br/>Barometer]
    MCU -- PWM x4 --> DRV[4x SI2302<br/>MOSFET drivers]
    BAT --> DRV
    DRV --> M[4x Brushed motors]
```

## 🔧 Key Components

| Function | Part | Notes |
|---|---|---|
| MCU | **ESP32-WROOM-32E** | Wi-Fi + BLE, dual-core |
| USB-UART | **CH340K** | BC817 auto-reset / boot circuit |
| Charger | **TP4056** | 1S LiPo charging with CHG / STDBY LEDs |
| Regulator | **AP2112K-3.3** | 600 mA low-dropout 3.3 V rail |
| Power path | **AO3401A**, SS34 | P-MOSFET switching, Schottky protection |
| Motor drivers | **SI2302** ×4 + PMEG40T10ER ×4 | Low-side switches with flyback diodes |
| IMU | **LSM6DS3** | 3-axis accelerometer + 3-axis gyroscope |
| Barometer | **LPS22HB** | Absolute pressure sensor for altitude |
| Connectors | USB-C 16P, JST-PH 2P, 4× motor sockets | |

## 🖼️ Gallery

| PCB Layout (F.Cu / B.Cu) | 3D View (Bottom) |
|:---:|:---:|
| <img src="%D7%AA%D7%9E%D7%95%D7%A0%D7%95%D7%AA/PCB_Layout.png" width="400"> | <img src="%D7%AA%D7%9E%D7%95%D7%A0%D7%95%D7%AA/3D_Viewer_BACK.png" width="400"> |

<details>
<summary><b>📐 Schematics (click to expand)</b></summary>

| Sheet | Preview |
|---|---|
| Top level | <img src="%D7%AA%D7%9E%D7%95%D7%A0%D7%95%D7%AA/Top_Level_Schematic.png" width="600"> |
| 01 – ESP32 Core & Connectivity | <img src="%D7%AA%D7%9E%D7%95%D7%A0%D7%95%D7%AA/01_Schematic.png" width="600"> |
| 02 – Power Management & LiPo | <img src="%D7%AA%D7%9E%D7%95%D7%A0%D7%95%D7%AA/02_Schematic.png" width="600"> |
| 03 – Motor Drivers & EMI Protection | <img src="%D7%AA%D7%9E%D7%95%D7%A0%D7%95%D7%AA/03_Schematic.png" width="600"> |
| 04 – Autonomous Flight Sensors | <img src="%D7%AA%D7%9E%D7%95%D7%A0%D7%95%D7%AA/04_Schematic.png" width="600"> |

</details>

## 📊 Board Stats

| Layers | Size | Thickness | Pads | Vias | Nets | Unrouted |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| 2 | 103 × 104 mm | 1.6 mm | 293 | 84 | 75 | **0** ✅ |

## 📁 Repository Structure

```
Drone_ESP32/
├── Drone_ESP32.kicad_pro / .kicad_sch / .kicad_pcb   # KiCad project (top level + PCB)
├── ESP32_Core.kicad_sch         # Sheet 01 – MCU, USB-UART, auto-reset
├── Power_Management.kicad_sch   # Sheet 02 – USB-C, LiPo charger, LDO
├── Motor_Drivers.kicad_sch      # Sheet 03 – 4x MOSFET motor drivers
├── Sensors_Suite.kicad_sch      # Sheet 04 – IMU + barometer
├── Gerbers_Production/          # Gerbers, drill files, JLCPCB zip
├── BOM.csv · CPL.csv            # JLCPCB assembly files
├── DATA SHEET/                  # Component datasheets
└── תמונות/                      # Renders & schematic exports
```

## 🏭 Manufacturing

1. Upload `Gerbers_Production/Drone_ESP32_JLCPCB.zip` to JLCPCB (2 layers, 1.6 mm).
2. Enable **PCB Assembly** and upload `BOM.csv` and `CPL.csv`.
3. Review component placement and rotation in the JLCPCB preview before ordering.

---

<div align="center">

Designed by **Asaf Aharon** · [GitHub](https://github.com/Asaf66) · [LinkedIn](https://linkedin.com/in/asaf-aharon-015595231)

</div>
