# 07. FPGA-Based LiDAR ISP Onboarding

- **Quick Links:** [Project Folder](https://drive.google.com/drive/folders/14Bk3T3FvfNHyUfI8Gu1VRx5ff47YclfH) | [LiDAR ISP GitHub Repo](https://github.com/RISC-M/LiDAR-Data-Processing-Accelerator) | [VLP-16 Puck Datasheet](https://drive.google.com/file/d/1oSLR_le6KBCPTmcanOFtHva6Yxfz9no_/view?usp=drive_link) | [DE10-Nano Getting Started Guide](https://www.intel.com/content/www/us/en/developer/articles/guide/terasic-de10-nano-get-started-guide.html) | [EECS 270 Course Page](https://www.eecs270.org/)
- **Contacts:** Bany, Dev

---

## 1. Prerequisites & Deliverables

> ⚠️ **Prerequisite Note:** EECS 270 (Digital Logic Design) or prior Verilog / RTL experience is required for this track.

### Project Goals
- Generate a real-time 2D occupancy grid feed compatible with Navigation and CV pipelines.
- Publish occupancy grid topics to ROS 2.
- Define physical mounting and electrical setup requirements for the Velodyne VLP-16 LiDAR.

---

## 2. Onboarding Assignments

### Assignment 1: Verilog Finite State Machine (FSM)
Complete the following HDLBits logic design problems and demonstrate completed testbenches:
- [HDLBits FSM Problem 1 (Exams/2013_q2afsm)](https://hdlbits.01xz.net/wiki/Exams/2013_q2afsm)
- [HDLBits FSM Problem 2 (Exams/2013_q2bfsm)](https://hdlbits.01xz.net/wiki/Exams/2013_q2bfsm)

---

## 3. Intel Quartus Environment & Bitstream Generation

1. Download **Intel Quartus Prime Lite Edition (v25.1)** or log in via CAEN workstations.
2. Clone repository:
   ```bash
   git clone https://github.com/RISC-M/LiDAR-Data-Processing-Accelerator.git
   ```
3. Open `fpga/lidar_accelerator.qpf` in Quartus.
4. Compile project: **Processing > Start Compilation** to generate `output_files/soc_system.sof`.
5. Convert `.sof` to `.rbf` (Raw Binary File for HPS bootloader):
   - Open **File > Convert Programming Files**.
   - Select **Raw Binary File (.rbf)**.
   - Choose `soc_system.sof`, enable **Parallel 16** mode under Options, and click **Generate**.
   - Or run CLI command:
     ```bash
     quartus_cpf -c -o bitstream_compression=on -o parallel_16=on soc_system.sof soc_system.rbf
     ```
6. Copy `soc_system.rbf` to the root directory of the DE10-Nano microSD card FAT32 partition. Ensure DIP switches are set for HPS auto-config (`MSEL[4:0] = 01010`).

---

## 4. DE10-Nano HPS Terminal Access

### Option 1: USB UART Serial Console
- **Windows:** Connect mini-USB cable, open PuTTY on assigned `COMx` port at `115200` baud.
- **macOS / Linux:**
  ```bash
  screen /dev/ttyUSB0 115200
  ```

### Option 2: Ethernet SSH
1. Connect DE10-Nano Ethernet port to your local router/switch.
2. Identify board IP address via serial console (`ifconfig`).
3. Connect over SSH:
   ```bash
   ssh root@<board-ip-address>
   ```

---

## 5. Running the Occupancy Grid Software

Navigate to the HPS source directory on the DE10-Nano, compile, and execute the runtime processing script:
```bash
cd hps
gcc -o lidar_script lidar_script.c
./lidar_script
```
*The script listens for incoming UDP packets from VLP-16 (port 2368), offloads packet conversion to the FPGA accelerator, and renders a live ASCII occupancy grid feed directly in the terminal.*
