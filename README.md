# 🧪 IoT-Based Sewage Monitoring System

## Project Overview 📈
This project presents an **IoT-based sewage monitoring system** designed to detect hazardous gases and monitor water levels in sewage environments. It aims to provide real-time alerts and data updates to concerned authorities, enhancing safety for sewage workers and facilitating timely municipal responses. The system integrates various sensors with an ESP32 microcontroller and utilizes the ThingSpeak IoT platform for data visualization and analysis.

---

## 🛠️ Components & Hardware
The system is built using the following key components:

* [cite_start]**ESP32 Microcontroller**: The brain of the system, responsible for processing sensor data and managing communication. [cite: 1]
* **Gas Sensors**:
    * **MQ-136 (H2S Gas Sensor)**: Detects Hydrogen Sulfide.
    * **MQ-4 (Methane Gas Sensor)**: Detects Methane (CH4).
    * **MG-811 (CO2 Gas Sensor)**: Detects Carbon Dioxide (CO2).
    * **MQ-137 (NH3 Gas Sensor)**: Detects Ammonia (NH3).
* [cite_start]**DHT11/DHT22 Sensor**: Measures temperature and humidity. [cite: 1, 44]
* **Ultrasonic Sensor (HC-SR04)**: Detects water levels for overflow detection.
* **SIM900A GSM Module**: Enables SMS alerts to registered mobile numbers.
* **LCD Display (16x2)**: Shows real-time sensor readings and system status.
* **Buzzer**: Provides an audible alert for detected hazards.

---

## ⚙️ System Architecture
The system's architecture can be summarized as follows:

* **Sensing Layer**: Multiple gas sensors (CO2, Methane, H2S, NH3), a DHT11/DHT22 sensor, and an ultrasonic sensor collect environmental data from the sewage.
* [cite_start]**Processing Layer (ESP32)**: The ESP32 microcontroller processes the analog and digital inputs from the sensors[cite: 1]. [cite_start]It calculates distance from the ultrasonic sensor [cite: 16, 52] [cite_start]and reads temperature and humidity from the DHT sensor[cite: 16, 49].
* **Communication Layer**:
    * **ThingSpeak Integration**: Sensor data (gas levels, temperature, humidity, water level) is uploaded to the ThingSpeak IoT platform for live monitoring and historical data analysis.
    * **GSM Module**: In case of detected gas thresholds or critical events, the GSM module sends SMS alerts to predefined mobile numbers (e.g., sewage workers, municipality).
* **Alert & Display Layer**:
    * [cite_start]An **LCD** provides local, real-time display of sensor values and system status. [cite: 17, 18, 53, 54]
    * [cite_start]A **buzzer** provides immediate audible alerts when gas levels exceed safe thresholds. [cite: 42, 64, 70, 76]

The system flow is visually represented in the architectural diagram.

---

## 🚀 Features
* **Multi-Gas Detection**: Monitors CO2, Methane, H2S, and NH3 gases, critical for identifying hazardous conditions in sewage.
* **Water Level Monitoring**: Detects sewage overflow using an ultrasonic sensor, preventing potential environmental hazards and infrastructure damage.
* [cite_start]**Environmental Monitoring**: Gathers temperature and humidity data. [cite: 16, 49]
* **Real-time Data Visualization**: Integrates with ThingSpeak for live plotting and analysis of sensor data.
* [cite_start]**Instant SMS Alerts**: Notifies designated personnel (sewage workers, municipality) via SMS when gas concentrations exceed safe limits [cite: 22, 23, 24, 25] [cite_start]or the system is ready[cite: 26, 92].
* [cite_start]**Audible Alarm**: Triggers a buzzer for immediate on-site alerts during hazardous conditions. [cite: 42, 64, 70, 76]
* [cite_start]**LCD Display**: Provides local, continuous display of all sensor readings. [cite: 17, 18, 53, 54]

---

## 🖼️ Visuals
* **Prototype**: A physical representation of the assembled hardware components.
* **3D Model**: A 3D rendered design of the system's enclosure.
* **SMS Output**: An example of the SMS alerts received from the system.
* **ThingSpeak Output**: Screenshots of the data charts on the ThingSpeak platform, showing trends for various parameters like CH4, NH3, CO2, H2S, Humidity, and Temperature.

---

## 💻 Code Details
The project includes Arduino sketches for both Arduino-based and ESP32-based implementations:

* [cite_start]**`IoT Based Sewage Monitoring Using Arduino.txt`**: This code uses the Arduino platform[cite: 44]. [cite_start]It initializes the LCD [cite: 47][cite_start], DHT sensor [cite: 47][cite_start], buzzer [cite: 47][cite_start], and gas sensors[cite: 47]. [cite_start]It continuously reads sensor data [cite: 50, 51][cite_start], calculates water distance [cite: 52][cite_start], and updates ThingSpeak[cite: 55]. [cite_start]It also includes logic for sending SMS alerts [cite: 58, 65, 71, 77] [cite_start]and triggering the buzzer [cite: 64, 70, 76] [cite_start]if gas levels exceed predefined thresholds[cite: 57, 64, 70, 76].
* [cite_start]**`IoT Based Sewage Monitoring Using Esp32.txt`**: This code is specifically for the ESP32[cite: 1]. [cite_start]It uses `WiFi.h` [cite: 1] [cite_start]and `ThingSpeak.h` [cite: 1] for internet connectivity and data uploads. [cite_start]Similar to the Arduino version, it reads sensor data (gas, temperature, humidity, distance) [cite: 15, 16] [cite_start]and sends it to ThingSpeak[cite: 18, 19]. [cite_start]It also handles SMS alerts via AT commands to the GSM module when gas levels surpass set limits. [cite: 22, 23, 24, 25]

---

## 🚀 Getting Started
1.  **Clone the repository**:
    ```bash
    git clone [https://github.com/your-username/sewage-monitoring.git](https://github.com/your-username/sewage-monitoring.git)
    ```
2.  [cite_start]**Hardware Setup**: Assemble the components as shown in `Prototype.jpg` and connect them according to the pin definitions in the Arduino sketches[cite: 5, 45, 46].
3.  **Software Setup**:
    * Open the appropriate Arduino sketch (`IoT Based Sewage Monitoring Using Arduino.txt` or `IoT Based Sewage Monitoring Using Esp32.txt`) in the Arduino IDE.
    * [cite_start]Install necessary libraries: `LiquidCrystal` [cite: 44][cite_start], `DHT sensor library` [cite: 1, 44][cite_start], `LiquidCrystal_I2C` (for ESP32) [cite: 2][cite_start], `WiFi` (for ESP32) [cite: 1][cite_start], `ThingSpeak` (for ESP32)[cite: 1].
    * [cite_start]Configure your Wi-Fi credentials (for ESP32) [cite: 2] [cite_start]and ThingSpeak API key [cite: 3] in the code.
    * [cite_start]Update the mobile numbers for SMS alerts in the code. [cite: 27, 30, 34, 37, 41, 59, 66, 72, 78, 91]
4.  **Upload the Code**: Select the correct board and port in the Arduino IDE and upload the code to your microcontroller.

---

## 📈 ThingSpeak Channel Configuration
The ThingSpeak platform is used for data visualization. You will need to create a new channel with the following fields:

* [cite_start]Field 1: CO2 Gas Sensor (or `G1_DATA` for ESP32) [cite: 18]
* [cite_start]Field 2: Methane Gas Sensor (or `G2_DATA` for ESP32) [cite: 18]
* [cite_start]Field 3: H2S Gas Sensor (or `G3_DATA` for ESP32) [cite: 19]
* [cite_start]Field 4: NH3 Gas Sensor (or `G4_DATA` for ESP32) [cite: 19]
* [cite_start]Field 5: Water Level (DistanceCm) [cite: 19]
* [cite_start]Field 6: Temperature (T) [cite: 19]
* [cite_start]Field 7: Humidity (H) [cite: 19]

[cite_start]Ensure your `myChannelNumber` [cite: 3] [cite_start]and `myWriteAPIKey` [cite: 3] in the ESP32 code match your ThingSpeak channel settings.

---

## 📞 SMS Alert Numbers
The system is configured to send SMS alerts to specific numbers. The provided code includes the following numbers for testing:
* [cite_start]`+919003721737` (for Arduino code) [cite: 59, 66, 72, 78, 91]
* [cite_start]`9655244999` (for ESP32 code) [cite: 27, 30, 34, 37, 41]

**Remember to replace these placeholders with your desired contact numbers before deploying the system.**

---

## 💡 Future Enhancements
* **Mobile Application Integration**: Develop a dedicated mobile app for real-time monitoring and control.
* **Cloud Database**: Utilize a more robust cloud database for long-term data storage and advanced analytics.
* **Predictive Maintenance**: Implement machine learning algorithms to predict potential failures or overflow events based on historical data.
* **Solar Power Integration**: Incorporate solar panels for sustainable and off-grid operation.
* **GPS Tracking**: Add a GPS module to track the location of multiple deployed monitoring units.

---

## 🛡️ License
This project is open-source and available under the [MIT License](LICENSE).

---

## 📞 Contact
For any queries or collaborations, feel free to reach out.
