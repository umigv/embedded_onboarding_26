# 03. ROS 2 Environment & Node Setup

- **Quick Links:** [ROS2 Docker VNC Setup Guide](https://docs.google.com/document/d/1HzKv-rk_55qC-WTXVjRAeTmDtkQDEhj7ZsPd90GykM8/edit?usp=sharing) | [Navigation Onboarding Repo](https://github.com/umigv/nav-onboarding-2025)
- **Contacts:** Chihyun, Bany, Jared

---

## 1. Environment Setup

Follow the Docker VNC setup guide to launch an Ubuntu 22.04 desktop container with **ROS 2 Humble** installed.

### macOS USB Serial Passthrough
If running Docker on macOS and interfacing with physical microcontrollers over USB serial, install `socat`:
```bash
brew install socat
```
Before launching your Docker container, open a terminal on your Mac and map your USB device (e.g., `/dev/cu.usbmodem1201`):
```bash
socat -d -d PTY,link=/tmp/seriallink,raw,echo=0 FILE:/dev/cu.usbmodem1201,b9600,raw,echo=0
```
Then mount `/tmp/seriallink` into your Docker container run command:
```bash
-v /tmp/seriallink:/dev/ttyUSB0 \
```

---

## 2. ROS 2 Talker & Listener Example

ROS nodes are independent processes performing computation. Talker nodes publish messages on topics (e.g., sensor data), while Listener nodes subscribe to topics to receive data. Refer to [ROS 2 Node Concepts](https://wiki.ros.org/ROS/Tutorials/UnderstandingNodes).

1. Open **Terminal 1** (Talker):
   ```bash
   ros2 run demo_nodes_cpp talker
   ```
2. Open **Terminal 2** (Listener):
   ```bash
   ros2 run demo_nodes_cpp listener
   ```
Observe the talker publishing messages and the listener receiving them.

---

## 3. Arduino Integration using ROS 2

Control an Arduino LED over ROS 2 topics using a custom Python bridge node (`arduino_bridge`).

### Arduino Sketch
Upload a sketch to your Arduino that reads characters over Serial (`Serial.read()`) at 9600 baud:
- `'1'` -> Turn LED ON (Pin 13 `HIGH`)
- `'0'` -> Turn LED OFF (Pin 13 `LOW`)

### Creating the ROS 2 Package
In your Docker terminal, execute:
```bash
mkdir -p ~/ros2_ws/src
cd ~/ros2_ws/src
ros2 pkg create --build-type ament_python arduino_bridge
```

Build the workspace:
```bash
cd ~/ros2_ws
colcon build --symlink-install
```

Auto-source ROS 2 workspace on terminal launch:
```bash
echo "source ~/ros2_ws/install/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

### Writing the ROS 2 Node (`led_control.py`)
Create the python script:
```bash
cd ~/ros2_ws/src/arduino_bridge/arduino_bridge/
touch led_control.py
```

Paste the following python implementation into `led_control.py`:
```python
import rclpy
from rclpy.node import Node
from std_msgs.msg import Bool
import serial

class ArduinoBridge(Node):
    def __init__(self):
        super().__init__('arduino_bridge')

        # Subscribe to topic /led_toggle
        self.subscription = self.create_subscription(
            Bool,
            'led_toggle',
            self.listener_callback,
            10
        )

        # Open serial connection to Arduino
        try:
            self.arduino = serial.Serial('/dev/ttyUSB0', 9600, timeout=1)
            self.get_logger().info("Connected to Arduino on /dev/ttyUSB0")
        except serial.SerialException:
            self.get_logger().error("Could not open serial port /dev/ttyUSB0")
            self.arduino = None

    def listener_callback(self, msg: Bool):
        if self.arduino:
            self.arduino.write(b'1' if msg.data else b'0')

def main(args=None):
    rclpy.init(args=args)
    node = ArduinoBridge()
    rclpy.spin(node)
    node.destroy_node()
    rclpy.shutdown()

if __name__ == '__main__':
    main()
```

### Configuring `setup.py` & `package.xml`
In `~/ros2_ws/src/arduino_bridge/setup.py`, update `console_scripts`:
```python
entry_points={
    'console_scripts': [
        "led_control = arduino_bridge.led_control:main",
    ],
},
```

In `~/ros2_ws/src/arduino_bridge/package.xml`, add dependencies inside `<package>`:
```xml
<depend>rclpy</depend>
<depend>std_msgs</depend>
```

### Building and Running
Rebuild workspace:
```bash
cd ~/ros2_ws
colcon build --symlink-install
```

Run node:
```bash
ros2 run arduino_bridge led_control
```

*Permissions Troubleshooting:*
If permissions are denied on `/dev/ttyUSB0` or `/dev/ttyACM0`:
```bash
sudo chmod 666 /dev/ttyUSB0
sudo usermod -a -G dialout $USER
```

Publish commands in another terminal:
```bash
# Turn ON LED
ros2 topic pub /led_toggle std_msgs/Bool "data: true"

# Turn OFF LED
ros2 topic pub /led_toggle std_msgs/Bool "data: false"
```

---

## 4. Multi-LED Challenge Project

Extend your `arduino_bridge` package to control **three independent LEDs**:
- Set up 3 distinct ROS 2 topics or a custom multi-channel message.
- Modify the Arduino sketch to handle unique control codes for each LED state.
- Test independent toggling of all 3 LEDs.
