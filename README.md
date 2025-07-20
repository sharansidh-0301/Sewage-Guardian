# 🌊 IoT-Based Sewage Monitoring System

## Project Overview 📜
This project presents an **IoT-based sewage monitoring system** designed to detect hazardous gases and monitor water levels within sewage environments. Its primary goal is to provide real-time alerts and data visualization to relevant personnel, enhancing safety for sewage workers and enabling timely responses from municipal authorities. The system integrates various sensors with an ESP32 microcontroller and leverages the ThingSpeak IoT platform for data streaming and analysis.

---

## 🛠️ System Components & Hardware
The system is built using the following key components:

* **ESP32 Microcontroller**: The central processing unit of the system.
* **Gas Sensors**:
    * **CO2 Gas Sensor (MG811)**: Detects Carbon Dioxide. [cite_start]The Arduino code refers to it as `sen1` [cite: 2] [cite_start]and the ESP32 code as `G1`[cite: 54].
    * **Methane Gas Sensor (MQ-4)**: Detects Methane (CH4). [cite_start]The Arduino code refers to it as `sen2` [cite: 2] [cite_start]and the ESP32 code as `G2`[cite: 54].
    * **H2S Gas Sensor (MQ-136)**: Detects Hydrogen Sulfide (H2S). [cite_start]The Arduino code refers to it as `sen3` [cite: 2] [cite_start]and the ESP32 code as `G3`[cite: 54].
    * **NH3 Gas Sensor (MQ-137)**: Detects Ammonia (NH3). [cite_start]The Arduino code refers to it as `sen4` [cite: 2] [cite_start]and the ESP32 code as `G4`[cite: 54].
* **DHT11 Sensor** (Arduino version) / **DHT22 Sensor** (ESP32 version): Measures temperature and humidity.
* **Ultrasonic Sensor**: Used for over-flow detection by measuring distance to the water level.
* **SIM900A GSM Module**: Enables sending SMS alerts to specified mobile numbers.
* **LCD Display**: A 16x2 character display for local concentration display and system status messages.
* **Alarm Buzzer**: Provides an audible alert when hazardous conditions are detected.

---

## ⚙️ System Architecture & Workflow
The system operates through a structured workflow:

1.  **Data Acquisition**:
    * Various gas sensors (CO2, Methane, H2S, NH3) are connected to the microcontroller to detect gas concentrations in the sewage environment.
    * A DHT sensor measures temperature and humidity.
    * An ultrasonic sensor monitors the water level for over-flow detection.
2.  **Central Processing (ESP32)**:
    * The ESP32 microcontroller receives and processes data from all connected sensors.
    * [cite_start]It reads analog values from the gas sensors [cite: 7, 8, 64] [cite_start]and digital values from the DHT and ultrasonic sensors[cite: 6, 9, 65].
3.  **Local Display**:
    * [cite_start]Sensor readings and system status messages are shown on a connected LCD display, providing real-time information locally[cite: 10, 11, 66, 67].
4.  **Data Transmission to IoT Platform**:
    * The collected sensor data (gas concentrations, water level, temperature, and humidity) is sent to the **ThingSpeak IoT platform**. This allows for live updates and historical plotting of the data, as seen in the ThingSpeak Output.
    * [cite_start]The Arduino code uses HTTP GET requests to update ThingSpeak fields[cite: 12, 45].
    * [cite_start]The ESP32 code uses `ThingSpeak.writeFields` to send data to the configured channel[cite: 68, 69].
5.  **Alerting Mechanisms**:
    * [cite_start]**SMS Alerts**: If any gas concentration exceeds predefined thresholds (e.g., CO2, CH4, NH3 > 300, H2S > 500)[cite: 14, 21, 26, 32], the SIM900A GSM module sends an SMS alert to registered mobile numbers. [cite_start]The system also sends an "project ready" SMS on startup[cite: 48, 77].
    * **Audible Alarm**: An alarm buzzer triggers an audible alert when gas thresholds are exceeded, providing immediate local notification.

---

## 🖼️ Visual Documentation
* **Architectural Representation**: A block diagram illustrating the overall system architecture and data flow.
* **Prototype**: A physical prototype demonstrating the assembled hardware components and their interconnections.
* **3D-Model Prototype**: A 3D rendered model of the system's intended enclosure.
* **ThingSpeak Output**: Screenshots showing the graphical representation of sensor data (CH4, NH3, CO2, H2S, Humidity, Temperature) as displayed on the ThingSpeak IoT platform.
* **SMS Output**: An example of the SMS messages received on a mobile device, including "project ready" and "Co2 DETECTED" alerts.

---

## 💻 Code Implementation
The project includes two main Arduino sketches demonstrating the implementation:

* **`IoT Based Sewage Monitoring Using Arduino.txt`**: This code is designed for Arduino boards. [cite_start]It sets up the LCD, DHT11, buzzer, and analog gas sensors (connected to A0-A3)[cite: 1, 2]. [cite_start]It also configures an ultrasonic sensor on pins 10 and 11[cite: 3]. [cite_start]The code includes functions for sending data to ThingSpeak and sending SMS alerts via a GSM module when gas levels exceed specific thresholds[cite: 12, 14].
* **`IoT Based Sewage Monitoring Using Esp32.txt`**: This code is tailored for the ESP32 microcontroller, utilizing its built-in Wi-Fi capabilities. [cite_start]It integrates with an I2C LCD [cite: 50, 51][cite_start], DHT22 sensor [cite: 50][cite_start], ultrasonic sensor [cite: 53][cite_start], and defines digital pins for gas sensors[cite: 54]. [cite_start]The code connects to Wi-Fi [cite: 59, 60] [cite_start]and then uses the ThingSpeak library to publish sensor data[cite: 68]. [cite_start]It also includes functions to send SMS alerts through the serial port to a connected GSM module if gas readings surpass set limits[cite: 71, 72, 73, 74].

---

## 🚀 Getting Started
1.  **Clone the Repository**:
    ```bash
    git clone [https://github.com/your-username/sewage-monitoring.git](https://github.com/your-username/sewage-monitoring.git)
    ```
2.  **Hardware Assembly**: Refer to the `Prototype.jpg` and the pin definitions within the `.txt` code files to correctly connect all sensors, modules, and the LCD to your ESP32 or Arduino board.
3.  **Software Setup**:
    * Open the appropriate `.txt` file (`IoT Based Sewage Monitoring Using Arduino.txt` or `IoT Based Sewage Monitoring Using Esp32.txt`) in the Arduino IDE.
    * Install required libraries: `LiquidCrystal`, `DHT sensor library`, `LiquidCrystal_I2C` (for ESP32), `WiFi` (for ESP32), and `ThingSpeak` (for ESP32).
    * **Configuration**:
        * [cite_start]For ESP32: Update the `ssid` and `password` variables with your Wi-Fi network credentials[cite: 51].
        * [cite_start]For both: Modify the `myChannelNumber` and `myWriteAPIKey` variables to match your ThingSpeak channel settings[cite: 52].
        * [cite_start]**Crucially**: Change the hardcoded phone numbers (`+919003721737` in Arduino [cite: 16, 48] [cite_start]and `9655244999` in ESP32 [cite: 76]) to your desired SMS alert recipients.
4.  **Upload Code**: Select the correct board and COM port in the Arduino IDE, then upload the sketch to your microcontroller.

---

## 📊 ThingSpeak Data Visualization
The project relies on ThingSpeak for remote data monitoring. To replicate the visualization, set up a ThingSpeak channel with the following field assignments:

* [cite_start]**Field 1**: CO2 Gas Sensor data (or `G1_DATA` for ESP32) [cite: 12, 45, 68]
* [cite_start]**Field 2**: Methane Gas Sensor data (or `G2_DATA` for ESP32) [cite: 12, 45, 68]
* [cite_start]**Field 3**: H2S Gas Sensor data (or `G3_DATA` for ESP32) [cite: 12, 45, 68]
* [cite_start]**Field 4**: NH3 Gas Sensor data (or `G4_DATA` for ESP32) [cite: 12, 45, 68]
* [cite_start]**Field 5**: Water Level (distanceCm) [cite: 12, 45, 68]
* [cite_start]**Field 6**: Temperature (t) [cite: 12, 45, 68]
* [cite_start]**Field 7**: Humidity (h) [cite: 12, 45, 68]

---

## 📞 SMS Alert Configuration
The system sends critical SMS alerts to pre-programmed mobile numbers. The numbers used in the provided code are:

* [cite_start]`+91987654310` for the Arduino implementation[cite: 16, 48].
* [cite_start]`+91987456321` for the ESP32 implementation[cite: 76].

**Please ensure these numbers are updated in the code to your specific contact numbers for proper functionality.**

---

## 🛡️ License
This project is open-source and available under the [MIT License](LICENSE).

---

## 📞 Contact
For any queries regarding this project, feel free to reach out.
