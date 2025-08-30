# MCU-Based Wireless Glove  

This project is a **wireless gesture-controlled glove** that streams **finger bends (flex sensors)** and **palm motion (IMU)** to a PC, where a Unity application animates a virtual hand in real time.  
- **STM32L031 MCU**: samples and processes sensor data.  
- **ESP32-WROOM**: handles wireless transmission via ESP-NOW.  
- **Python bridge**: ingests and calibrates data, then forwards it to Unity.  
- **Unity C# script**: applies finger and palm movements to a 3D hand model.  

👉 For detailed technical documentation (hardware schematics, PCB design, and system explanation), please see the [Docs/](./Docs) folder.  

---

## 📂 Repository Structure  

MCU-Based-Wireless-Glove/
│
├── Docs/ # Project documentation (ECE395 Final Report + notes)
├── pcb-files/ # PCB schematics, layouts, and related design files
├── src/ # Source code for firmware, PC bridge, and Unity listener
│ ├── stm32/ # STM32 firmware (ADC, IMU SPI, UART output)
│ ├── esp32/ # ESP32 firmware (ESP-NOW wireless bridge, optional IMU polling)
│ ├── python/ # PC-side scripts (serial ingest, calibration, TCP forward)
│ └── unity/ # Unity C# listener scripts (GloveReceiver.cs)
├── placeholder/ # Temporary / unused files (safe to ignore)
├── LICENSE # License information
└── README.md # Project overview (this file)

- **Docs/** – contains the final project report and supporting documents. Start here if you want to understand the full design.  
- **pcb-files/** – all hardware-related design files for the custom PCB.  
- **src/** – source code divided into:  
  - **stm32/** – firmware for STM32L031 MCU (flex sensor ADC, IMU via SPI, UART data framing).  
  - **esp32/** – firmware for ESP32 (wireless data forwarding using ESP-NOW, with optional IMU fallback).  
  - **python/** – PC bridge (`main.py` and helpers) that parses UART data, calibrates sensor values, and forwards JSON over TCP.  
  - **unity/** – Unity scripts (e.g., `GloveReceiver.cs`) that apply incoming data to animate a 3D hand model.  
- **placeholder/** – unused or staging area, not critical to the project.  

---

## ▶️ How It Works  

1. **Sensor acquisition**  
   - Flex sensors + op-amp circuits measure finger bends.  
   - IMU (ICM-20948) provides palm orientation and motion data.  
   - STM32 samples all signals and sends data over UART to the ESP32.  

2. **Wireless bridge**  
   - ESP32 transmits processed sensor data wirelessly to the PC via ESP-NOW.  

3. **PC bridge (Python)**  
   - Parses UART data, calibrates values, and forwards JSON packets over TCP.  

4. **Unity listener**  
   - Receives the data and animates a virtual hand in Unity with low latency.  

---

## 🛠️ Getting Started  

- Build and flash STM32 firmware (inside `src/`).  
- Flash ESP32 firmware (inside `src/`).  
- Run the Python script to ingest sensor data and forward to Unity.  
- Import the Unity C# script into your project to animate the hand.  

**Dependencies:**  
- STM32CubeIDE (or equivalent toolchain)  
- ESP-IDF for ESP32  
- Python 3.x with `pyserial`  
- Unity (2021 LTS or newer recommended)  

---

## 📖 Documentation  

Full documentation and project report can be found in [Docs/](./Docs). This includes:  
- Hardware schematics & PCB design decisions  
- Firmware architecture  
- Python/Unity pipeline  
- Performance metrics and improvements  

---
