# 02. Arduino Onboarding & Projects

- **Quick Links:** [CS Intro Guide](https://github.com/umigv/embedded_onboarding/blob/main/cs_intro.md) | [Git Intro Guide](https://github.com/umigv/embedded_onboarding/blob/main/git_intro.md)
- **Contacts:** Dev, Bany, Jared

---

## 1. Prerequisite Knowledge & Setup

Before getting started, ensure you are familiar with:
- Basic C/C++ programming concepts (`if` statements, `for`/`while` loops, functions). If you need a refresher, check out the [CS Intro Guide](https://github.com/umigv/embedded_onboarding/blob/main/cs_intro.md).
- Git basics.

### Microcontroller Setup
1. Launch Arduino IDE.
2. Connect your Arduino (Uno, Mega, or Nano) to your computer via USB.
3. Select board: Go to **Tools > Board > Arduino AVR Boards** and select your board (e.g., *Arduino Uno* or *Arduino Mega 2560*).
4. Select port: Go to **Tools > Port** and choose the COM/serial port connected to your Arduino.

---

## 2. Core Concepts

### Default Functions
When creating a new sketch, Arduino pre-populates two functions:
- `void setup()`: Runs once when the board powers up or resets. Used for initializing pins, baud rates, and sensors.
- `void loop()`: Runs continuously in an infinite loop after `setup()` finishes.

### Pins & Breadboard Basics
- Microcontrollers have GPIO pins (Digital, Analog, PWM, Power/GND headers).
- Breadboards provide internal connected rails for easy circuit prototyping. Check out this [Breadboard Basics Video Tutorial](https://www.youtube.com/watch?v=fq6U5Y14oM4) if needed.

---

## 3. Onboarding Projects

### Project 1: Blink
- Follow the official [Arduino Blink Tutorial](https://www.arduino.cc/en/Tutorial/BuiltInExamples/Blink).
- Turn on/off the onboard LED (Pin 13) with delays.

### Project 2: HC-SR04 Ultrasonic Distance Sensor
- Follow the [HC-SR04 Ultrasonic Sensor Tutorial](https://lastminuteengineers.com/arduino-sr04-ultrasonic-sensor-tutorial/).
- Read distance values over Serial Monitor (`Serial.println()`).

### Project 3: RGB LED Dimming with PWM
- Refer to [Arduino Analog Output (PWM) Guide](https://docs.arduino.cc/learn/microcontrollers/analog-output).
- Write an Arduino sketch using `analogWrite()` to smoothly dim and fade an RGB LED through different color spectrums.

### Project 4: ODrive Motor Controller Setup & Motion
- Connect the Arduino to an ODrive motor controller.
- Write a sketch sending UART/CAN serial commands to command motor spin.

### Project 5: Motor Exploration & Integration
- Connect external motors / encoders to the Arduino.
- Measure position/speed feedback and run basic motor speed control algorithms.

---

## 4. Tips & Best Practices
- **Ask Questions:** Reach out to mentors whenever you run into issues.
- **Utilize Resources:** Search Stack Overflow, official documentation, and AI tools for debugging.
- **Collaborate:** Work in pairs or small groups—simulating real team project workflows.
