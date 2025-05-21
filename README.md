# 🌊 Smart Water Quality Sensor (SMD-Based, Offline, Threshold-Driven)

This project is a fully open-source, battery-powered smart water quality sensor designed for **rural and underserved communities**. It measures key water quality parameters—**TDS**, **turbidity**, **temperature**, and **bacteria presence**—using threshold logic and displays results via **RGB LEDs**. The system is built entirely with **SMD components**, designed for **low-cost field deployment**, **no internet dependency**, and **offline reliability**.

---

## 🔧 Features

- ⚡ Powered by rechargeable Li-Ion battery (with onboard TP4057 charge controller)
- 💧 Sensors:
  - Total Dissolved Solids (TDS) via op-amp amplifier
  - Turbidity via IR emitter + phototransistor
  - Temperature via NTC thermistor
  - Bacteria detection via passive test strip + photoresistor
- 🌈 RGB status indication using WS2812B (safe, caution, unsafe)
- 📦 All-SMD design — no through-hole components
- 💾 Optional microSD data logging in SPI mode
- 🧠 Threshold-based logic (no AI or connectivity required)
- 🌞 Power-flag compliant, single-board schematic in KiCad

---

## 📐 KiCad Design Breakdown

### 🧠 Microcontroller
- **ESP32-S3-WROOM-1**
- Handles sensor reading, LED logic, and optional data logging
- Powered from LDO output (`VCC_3V3`)

### 🔋 Power Subsystem
- **TP4057** for safe battery charging (1-cell LiPo)
- **Schottky diode** for backflow protection
- **Fuse** and `VBAT_RAW`, `VBAT`, `VCC_RAW` rail structure
- **AMS1117-3.3 LDO** for regulated logic power

### 💧 Sensor Suite
- **TDS Amplifier**: LM321 op-amp with divider and feedback resistor
- **Turbidity**: IR LED with current-limiting resistor + phototransistor + pull-up
- **Temperature**: Voltage divider using 10kΩ NTC thermistor
- **Bacteria Indicator**: Passive test strip read by photoresistor

### 🌈 Output Interface
- **WS2812B RGB LED**
- Powered by `VCC_RAW` with data input from ESP32
- Series 330Ω resistor and 100uF decoupling cap included

### 💾 Data Logging (Optional)
- microSD card socket
- SPI mode with pull-ups and bypass caps

---

## 🧩 Component Overview

| Category           | Components |
|--------------------|------------|
| MCU                | ESP32-S3-WROOM-1 |
| Power Management   | TP4057, AMS1117-3.3, 1A Fuse, SS14 Schottky |
| Sensing            | LM321, IR LED, Phototransistor, NTC Thermistor, Photoresistor |
| Display/Output     | WS2812B RGB LED |
| Data Storage       | microSD card in SPI mode |
| Passive Components | 0603/1206 SMD resistors and capacitors |

---

## 🛠️ Assembly Notes

- All components use **standard SMD footprints** (0603 resistors/caps, SOT-23 packages, SMA diodes)
- Designed to be fabricated via JLCPCB or equivalent
- Avoids external connectors (except SD card and charging pads)
- Fully KiCad 7+ compatible

---

## 📁 Directory Structure

```
/kicad_project/
├── smart_water_sensor.kicad_pro
├── smart_water_sensor.kicad_sch
├── smart_water_sensor.kicad_pcb
├── symbols/
├── footprints/
└── README.md
```

---

## 🧠 Logic Overview (Thresholds Only)

All logic is hardcoded using `if/else` conditions based on safe ranges:

```c
if (TDS > 600 || turbidity > 5 || temperature > 35 || bacteria_detected) {
    showLED("RED");  // Unsafe
} else if (TDS > 400 || turbidity > 2) {
    showLED("YELLOW");  // Caution
} else {
    showLED("GREEN");  // Safe
}
```

---

## 📜 License

This project is licensed under the **MIT License**. Open-source contributions and field deployment adaptations are encouraged.

---

## 🧪 Acknowledgments

- Designed with humanitarian deployment in mind
- Inspired by the need for **off-grid diagnostics** in low-infrastructure regions
- Powered by open-source hardware and software principles

---

## Preview
![image](https://github.com/user-attachments/assets/7d83a0fa-14bb-4bcd-adbd-d9db0ba7ea0e)

---

**Built with ❤️ using KiCad, creativity, and purpose.**
