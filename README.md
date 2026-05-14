# ESP 32 Real Time Bluetooth TempMonitor 
## By: Anthony Taylor 
### [Project Code GitHub Repository](https://github.com/TaylorA293/CS-210-Final-Project-Source-Code/tree/main)

### Introduction:
Monitoring the temperature of our surroundings is critical in today's world. Whether that be maintaining the integrity of medical cold supply chains, or making sure that the performance of high density server environments are optimized. Constant temperature monitoring is essential because minor temperature changes can lead to significant degradation of computer system hardware, spoilage of food products and medications, and potentially compromised experimental data. It is these reasons that make temperature monitoring a necessity. This project addresses the need for a quick time temperature tracking solution through the use of `ESP 32 Real Time Bluetooth TempMonitor`. I created this system to use the Bluetooth connectivity of the ESP 32 board along with the thermistor to track and display real time temperature data. It allows the user to remotely monitor the temperature conditions of the environment without physical interaction, making sure the data is always within reach. This webpage teaches you how to build the `ESP 32 Real Time Bluetooth TempMonitor` from scratch.

<br>

---

### System Overview:

<img src="CS 210 Project Diagram.jpg" width="100%" alt="System Overview Diagram" style="max-width: 1000px; display: block; margin: 0 auto;">

The diagram above shows the three main components (excluding stuff like wires and resistors) working together. On the left is the thermistor, which is a temperature sensor that is able to detect heat in the environment and turn it into an electrical signal that the ESP32 can use. The ESP32, which is in the center of the diagram, is the microcontroller that receives the signal from the thermistor and converts it to a readable temperature value. It also stores the values with timestamps and checks if it's above a set threshold, and processes the commands from the master device (your phone, laptop, tablet, etc), which is on the right of the diagram. This user interface is where you can input your commands (START, STOP, HISTORY, SHUTDOWN, and SET_THRESHOLD). The thermistor connects directly to the ESP32, the ESP32 communicates wirelessly to your device, and displays the output depending on the command from the master device. 

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

Once you have the hardware completed and built, you can upload the code to it. You can find the source code for the TempMonitor at the beginning and in the "Source Code" portion of this webpage. 

<br>

---

### Source Code: 

### [Project Code GitHub Repository](https://github.com/TaylorA293/CS-210-Final-Project-Source-Code/tree/main)

### Here are some interesting parts of the source code: 

### Real Time Temperature Calculation

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
**Interesting Concept:** The `log()` function and Steinhart-Hart equation converts the values from the thermistor to linear temperature readings. This gives us the temperature readings that we see in the Serial Monitor. 

<br>

### Threshold Alerting

The System Continuously Monitors The Temperature and Sends Alerts:

```cpp
void checkTemperatureAlert(double temp) {
  if (temp > tempThreshold) {
    String alert = "🔥 ALERT! Temp: " + String(temp, 1) + 
                   "°C (Threshold: " + String(tempThreshold, 1) + "°C)";
    sendBLE(alert);
  }
}
```

**Interesting Concept:** This is a continuous loop that will constantly check the temperature reading and will display a warning message if the temperature crosses this threshold. Conditional monitoring is essential for device and server management. Devices auto check conditions and alert users without manual intervention.

<br> 

### User Command Input 

Users Can Control The System with Bluetooth:

```cpp
if (command == "START") {
  isLogging = true;
  readingCount = 0;
  sendBLE("✓ Logging started!");
}
else if (command == "STOP") {
  isLogging = false;
  sendBLE("✓ Logging stopped!");
}
else if (command == "HISTORY") {
  // Send all logged readings with statistics
}
else if (command == "SET_THRESHOLD:25") {
  tempThreshold = 25.0;
}
```

**Interesting Concept:** Allows for the user to input commands to the board to have the desired outcome. This allows for easy control of the system with little manual labor. 

<br>

---

### Demonstration:

<img src="Demonstration Screenshot.png" width="100%" alt="System Overview Diagram" style="max-width: 1000px; display: block; margin: 0 auto;">

Once the code is uploaded, open the serial monitor, and you should see something that looks like the picture above. This will run on a constant loop, displaying the current temperature of the environment. You can test it by placing your fingers on the thermistor and watching the temperature rise. Once you confirm that it is working, you can connect your device to it using the Bluetooth app of your choice. Look for "Tempmonitor_ESP32" and press connect. You should see "Phone Connected!" display in the Serial Monitor. From here, you can input commands such as START, STOP, HISTORY, and SET_THRESHOLD, and view what happens. 

<br>

--- 

### Key Features of The TempMonitor:

- ✓ Real-time temperature reading every second.
- ✓ Wireless Bluetooth communication with any device.
- ✓ Interactive commands (START, STOP, HISTORY, and SET_THRESHOLD) from the master device.
- ✓ Automatic temperature alerts when the temperature threshold is exceeded.
- ✓ Configurable alert thresholds via Bluetooth.
- ✓ Data logging with timestamps for potential analysis.
- ✓ Power management with low-power sleep modes.

<br>

---


### References: 
- [Freenove Thermistor Tutorial](https://docs.freenove.com/projects/fnk0083/en/latest/fnk0083/codes/C/13_Thermistor.html) — Guide for reading NTC thermistors with ESP32

- [Freenove BLE Data Passthrough](https://docs.freenove.com/projects/fnk0083/en/latest/fnk0083/codes/C/27_Bluetooth.html#project-bluetooth-low-energy-data-passthrough) — BLE communication setup

- [Espressif ESP32 ADC Documentation](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-reference/peripherals/adc.html) — Analog to digital conversion

- [Espressif BLE API Reference](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-reference/bluetooth/ble.html) — Bluetooth Low Energy API

- [Arduino Language Reference](https://www.arduino.cc/reference/) — Built in functions and libraries which help in the coding process.

- [Random Nerd Tutorials - ESP32 Bluetooth](https://randomnerdtutorials.com/esp32-bluetooth-classic-arduino-ide/) — Best practices and tutorials on how to use the ESP32 Bluetooth.
  
- [Stack Overflow - C Programming Reference](https://stackoverflow.com/questions) - Good for assistance in coding and help when stuck.

- [Claude - Artificial Intelligence Assistant](https://claude.ai/new) - Good for proofreading and explaining how certain aspects of the board work.

- [Github - Project Repository and Ideas](https://github.com/) - Good to look for inspiration, as well as material to work with.

- [Visual Studio Code IDE and AI Copilot](https://code.visualstudio.com/) - Good code compiler along with AI assistive code generation. Also reviews code and suggests edits. 

<br>
