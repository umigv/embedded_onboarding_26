# 06. Kraken Motor Controller Guide

- **Contacts:** Ethan, Ruey, Jared

---

## 1. Overview & Guidelines

The Kraken X60 brushless motor with integrated Talon FX controller provides direct CAN-bus motor control. The goal of this onboarding section is to establish consistent motor bring-up and configuration.

### Metrics of Consistency
1. Systematically yield a stable working status LED mode (**solid orange**) upon power-up.
2. Maintain a 100% reliable startup script running on boot.
3. Install a physical **120 Ω CAN bus termination resistor** (replacing temporary 1000 Ω resistors).

---

## 2. Startup & Operation Procedure

1. **Linux SocketCAN Initialization:**
   Bring up the CAN interface with root permissions:
   ```bash
   sudo ip link set can0 type can bitrate 500000
   sudo ip link set up can0
   ```
   Verify CAN activity:
   ```bash
   cansend can0 123#112233
   candump can0
   ```

2. **Hardware Target Initialization:**
   In Python (with `sudo` privileges), target the hardware control script. 
   - Initial LED state: *Alternating Orange*.
   - Post-initialization LED state: *Solid Orange* (Ready).

3. **CTRE Phoenix Tuner Setup:**
   Use Phoenix Tuner (Windows or Mobile) to set CAN Device IDs, monitor diagnostics, and push firmware updates to Talon FX units.
