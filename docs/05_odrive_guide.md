# 05. ODrive Motor Controller Guide

- **Quick Links:** [ODrive v3.6 Documentation](https://docs.odriverobotics.com/v/0.5.6/getting-started.html) | [ODrive S1 GUI Configuration Wizard](https://gui.odriverobotics.com/configuration) | [Embedded Stack Firmware Repo](https://github.com/umigv/embedded_stack)
- **Contacts:** Bany, Jared

---

## 1. Introduction to ODrive

ODrive is a high-performance open-source motor controller for Brushless DC (BLDC) motors. Utilizing high-resolution encoder feedback, it allows precise position, velocity, and torque control across two independent motor axes (`axis0` and `axis1`). Communication interfaces include USB, UART, and CAN bus.

---

## 2. Installation & Setup

### Installing `odrivetool`

**macOS:**
```bash
brew install python libusb
pip3 install --upgrade odrive
```

**Windows:**
1. Install [Anaconda](https://www.anaconda.com/download).
2. Open Anaconda Prompt and execute:
   ```cmd
   pip install --upgrade odrive
   ```

### Launching `odrivetool`
Connect ODrive via USB, power up the board, and run:
```bash
odrivetool
```
*(For ODrive S1, you can also use the web-based [ODrive GUI Wizard](https://gui.odriverobotics.com/configuration)).*

---

## 3. Motor Calibration & Motion Control

Run calibration on `axis0` (or `axis1` depending on drive side):

### Step 1: Full Calibration Sequence
```python
odrv0.axis0.requested_state = AXIS_STATE_FULL_CALIBRATION_SEQUENCE
```
*The motor will beep, slowly turn one direction, pause, and rotate in reverse.*

### Step 2: Enable Closed Loop Control
```python
odrv0.axis0.requested_state = AXIS_STATE_CLOSED_LOOP_CONTROL
```
*The motor holds position; manual rotation should encounter active resistance.*

### Step 3: Velocity Control Mode
```python
odrv0.axis0.controller.config.control_mode = CONTROL_MODE_VELOCITY_CONTROL
odrv0.axis0.controller.input_vel = 2  # Speed in turns/second
```

---

## 4. Key ODrive Commands

| Command | Function |
| :--- | :--- |
| `dump_errors(odrv0)` | Print active system and axis error codes |
| `odrv0.clear_errors()` | Clear active error flags |
| `odrv0.axis0.controller.input_pos = <turns>` | Command absolute target position |
| `odrv0.axis0.controller.input_vel = <turns_per_sec>` | Command target velocity |
| `odrv0.axis0.controller.input_torque = <Nm>` | Command target torque in Nm |
| `odrv0.axis0.motor.config.current_lim = <Amps>` | Set motor current limit |
| `odrv0.axis0.controller.config.vel_limit = <val>` | Set maximum velocity limit |
| `odrv0.config.enable_brake_resistor = True` | Enable power dissipation brake resistor |
| `odrv0.axis0.motor.config.pole_pairs = <count>` | Set motor rotor pole pair count |
