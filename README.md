# ESP 32 Real Time Bluetooth TempMonitor 
## By: Anthony Taylor 
### [Project Code GitHub Repository](#code)

### Introduction:
Monitoring the temperature of our surroundings is critical in today's world. Whether that be maintaining the integrity of medical cold supply chains, or making sure that the performance of high density server environments are optimized. Constant temperature monitoring is essential because minor temperature changes can lead to significant degradation of computer system hardware, spoilage of food products and medications, and potentially compromised experimental data. It is these reasons that make temperature monitoring a necessity. This project addresses the need for a quick time temperature tracking solution through the use of `ESP 32 Real Time Bluetooth TempMonitor`. I created this system to use the Bluetooth connectivity of the ESP 32 board along with the thermistor to track and display real time temperature data. It allows the user to remotely monitor the temperature conditions of the environment without physical interaction, making sure the data is always within reach. This webpage teaches you how to build the `ESP 32 Real Time Bluetooth TempMonitor` from scratch.

<br>

---

### System Overview:

<img src="CS 210 Project Diagram.jpg" width="100%" alt="System Overview Diagram" style="max-width: 1000px; display: block; margin: 0 auto;">

The diagram above shows the three main components (excluding stuff like wires and resistors) working together. On the left is the thermistor, which is a temperature sensor that is able to detect heat in the environment and turn it into an electrical signal that the ESP32 can use. The ESP32, which is in the center of the diagram, is the microcontroller that receives the signal from the thermistor and converts it to a readable temperature value. It also stores the values with timestamps and checks if it's above a set threshold, and processes the commands from the master device (your phone, laptop, tablet, etc), which is on the right of the diagram. This user interface is where you can input your commands (START, STOP, HISTORY, RESET, SHUTDOWN, and SET_THRESHOLD). The thermistor connects directly to the ESP32, the ESP32 communicates wirelessly to your device, and displays the output depending on the command from the master device. 

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

### How to Build: 
In order to build the `ESP 32 Real Time Bluetooth TempMonitor`, you start by finding the 3.3V and GRND pins on the board, which will be labeled to the right of the board. Using one of the jumper wires, connect it in the middle row of the pin marked 1 on the board. In the same row, connect that same wire into a port further down the board. Above the port where you placed the wire, place one end of the resistor; place the other end of the resistor in the GRND row in the same column. Then place the thermistor one away from the first wire you placed, but in the same row. Connect that first wire with one leg of the thermistor with another wire. Connect the other leg of the thermistor with a wire and link it to GRND. The final result should look like this:

<img src="CS Project Build IRL.PNG" width="100%" alt="System Overview Diagram" style="max-width: 1000px; display: block; margin: 0 auto;">

<img src="CS Project Build Diagram.png" width="100%" alt="System Overview Diagram" style="max-width: 1000px; display: block; margin: 0 auto;">

Once you have the hardware completed and built, you can upload the code to it. You can find the source code for the TempMonitor at the beginning and end of this webpage. 

<br>

---

### Source Code: 

### Here are some interesting parts of the source code. 

Thermistor Temperature Calculation using the Steinhart-Hart Equation: 

```cpp
double readTemperature() {
  int adcValue = analogRead(PIN_ANALOG_IN);
  double voltage = (float)adcValue / 4095.0 * 3.3;
  double Rt = 10 * voltage / (3.3 - voltage);
  
  // Steinhart-Hart: converts resistance to absolute temperature
  double tempK = 1 / (1 / (273.15 + 25) + log(Rt / 10) / 3950.0);
  double tempC = tempK - 273.15;  // Kelvin to Celsius
  return tempC;
}
```
**Interesting Concept:** The `log()` function and Steinhart-Hart equation convert the values from the thermistor to linear temperature readings. This gives us the temperature readings that we see in the Serial Monitor. 
<br>

---

### Key Features of The TempMonitor:

- ✓ Real-time temperature reading every second.
- ✓ Wireless Bluetooth communication with any device.
- ✓ Interactive command system (START, STOP, HISTORY, RESET) from master device.
- ✓ Automatic temperature alerts when the temperature threshold is exceeded.
- ✓ Configurable alert thresholds via Bluetooth.
- ✓ Data logging with timestamps for potential analysis.
- ✓ Power management with low-power sleep modes.

<br>

---


### Source Code:



<br>

---

### References: 
