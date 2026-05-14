# ESP 32 Real Time Bluetooth TempMonitor 
## By: Anthony Taylor 
### [Project Code GitHub Repository](#code)

### Introduction:
Monitoring the temperature of our surroundings is critical in today's world. Whether that be maintaining the integrity of medical cold supply chains, or making sure that the performance of high density server environments are optimized. Constant temperature monitoring is essential because minor temperature changes can lead to significant degradation of computer system hardware, spoilage of food products and medications, and potentially compromised experimental data. It is these reasons that make temperature monitoring a necessity. This project addresses the need for a quick time temperature tracking solution through the use of `ESP 32 Real Time Bluetooth TempMonitor`. I created this system to use the Bluetooth connectivity of the ESP 32 board along with the thermistor to track and display real time temperature data. It allows the user to remotely monitor the temperature conditions of the environment without physical interaction, making sure the data is always within reach. This webpage teaches you how to build the `ESP 32 Real Time Bluetooth TempMonitor` from scratch.

<br>

---

### System Overview:

<img src="CS 210 Project Diagram.jpg" width="100%" alt="System Overview Diagram" style="max-width: 1000px; display: block; margin: 0 auto;">
<br>

---


### Materials Needed:

### Hardware: 
**1 × ESP32 Development Board with Breadboard Attached**
- (ESP32-S3, ESP32-WROOM) Must have WiFi and Bluetooth capabilities.

**1 × Thermistor (10kΩ)**
- Temperature sensor for temperature monitoring and input.

**1 × Resistor (10kΩ)**
- Resistor for the voltage divider circuit.

**1 × USB Cable**
- To upload the code and supply the board with power.

**3 × M/M Jumper Wires**
- For making connections between the board and external hardware.

### Software:
**Arduino IDE (v1.8.19+)**
- Download from [arduino.cc](https://www.arduino.cc/en/software)

**ESP32 Board Package**
- Install via Tools → Board Manager → "esp32" by Espressif Systems

**Bluetooth Terminal App**
- Android: "Serial Bluetooth Terminal" by Kai Morich (free)
- IOS: "LightBlue" by Punch Through (free)
  
<br>

---

### Key Features:

- ✓ Real-time temperature reading every second.
- ✓ Wireless Bluetooth communication with any device.
- ✓ Interactive command system (START, STOP, HISTORY, RESET).
- ✓ Automatic temperature alerts when the temperature threshold is exceeded.
- ✓ Configurable alert thresholds via Bluetooth.
- ✓ Data logging with timestamps for potential analysis.
- ✓ Power management with low-power sleep modes.

<br>

---


### Conclusion:
