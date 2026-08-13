# Embedded Hardware Onboarding 2026-2027

Welcome to the **UMIGV Hardware / Embedded Team Onboarding** repository! This documentation serves as a comprehensive guide for new members joining the hardware team, covering embedded systems, microcontrollers, ROS 2, PCB design with Altium, motor control with ODrive & Kraken, and FPGA-based LiDAR processing.

---

## 📚 Table of Contents

1. [Quick Start & Setup](docs/01_quick_start.md)
   - Overview & expectations
   - Software installation guide (VS Code, Arduino IDE, STM32CubeIDE, Git, Anaconda)

2. [Arduino Onboarding & Projects](docs/02_arduino_onboarding.md)
   - Pre-requisites & setup
   - Basic concepts (setup vs loop, breadboard, pinouts)
   - Projects 1–5 (Blink, Ultrasonic Sensor, RGB LED Dimming, ODrive connection, Motor exploration)

3. [ROS 2 Environment & Node Setup](docs/03_ros2_onboarding.md)
   - Docker VNC & Ubuntu 22.04 / ROS 2 Humble environment setup
   - macOS USB serial passthrough (`socat`)
   - ROS 2 Talker & Listener tutorial
   - ROS 2 Arduino Bridge Project (`arduino_bridge` package & LED control)
   - Multi-LED ROS 2 challenge project

4. [Altium Designer PCB Tutorial & Troubleshooting](docs/04_altium_pcb_tutorial.md)
   - Introduction to PCB design & Altium Designer
   - Downloading & setting up student licenses
   - Git integration for Altium projects
   - Creating Schematic Symbols & PCB Footprints
   - Designing Schematics & PCB Routing (traces, layers, copper pour, vias)
   - Documentation & Gerber / NC Drill file generation for JLCPCB
   - Mandatory ARV Logo addition & Altium Keyboard Shortcuts reference table
   - Starter projects (Temperature sensor, ESP32 matching, 2-Channel Relay)

5. [ODrive Motor Controller Guide](docs/05_odrive_guide.md)
   - Overview of ODrive v3.6 & ODrive S1
   - `odrivetool` installation & GUI Wizard configuration
   - Step-by-step Calibration sequence (full calibration, closed-loop velocity control)
   - Pinout documentation & key ODrive CLI commands

6. [Kraken Motor Controller Guide](docs/06_kraken_guide.md)
   - Performance goals & metrics of consistency
   - Linux SocketCAN setup & startup procedure
   - Phoenix Tuner configuration & firmware updates

7. [FPGA-Based LiDAR ISP Onboarding](docs/07_lidar_fpga_onboarding.md)
   - Requirements & EECS 270 prerequisite info
   - Verilog Finite State Machine (FSM) coding exercises (HDLBits)
   - Intel Quartus Lite setup & `LiDAR-Data-Processing-Accelerator` repository compilation
   - Converting `.sof` to `.rbf` bitstream & DE10-Nano SD card setup
   - HPS (ARM Processor) terminal access (Serial console & SSH)
   - Compiling and executing `lidar_script.c` live ASCII occupancy grid feed

---

## 🛠️ Quick Reference & Links

- **Main Repository:** [umigv/embedded_onboarding](https://github.com/umigv/embedded_onboarding)
- **Firmware Repository:** [umigv/embedded_firmware](https://github.com/umigv/embedded_firmware)
- **PCB Stack Repository:** [umigv/Embedded_Stack_ROS2](https://github.com/umigv/Embedded_Stack_ROS2)
- **FPGA LiDAR Repository:** [RISC-M/LiDAR-Data-Processing-Accelerator](https://github.com/RISC-M/LiDAR-Data-Processing-Accelerator)
