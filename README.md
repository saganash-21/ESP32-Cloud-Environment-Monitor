# 🌍 ESP32 Environmental Monitor with Arduino IoT Cloud

This project uses an **ESP32** to monitor a room's environment in real-time.  
It tracks **temperature**, **humidity**, **light**, and **sound levels**, and sends the data to the **Arduino IoT Cloud** for a live, interactive dashboard.  
The system also provides **local visual (LED)** and **audible (buzzer)** alerts for high temperatures or low light.

---

## 📈 Live Dashboard

The dashboard provides a live view of all sensors, as well as historical data in charts.  
It also features a **"Mute" switch** to remotely silence the on-device buzzer.

📸 **Dashboard Preview:**  
![Dashboard Image](https://github.com/saganash-21/ESP32-Cloud-Environment-Monitor/blob/main/MEDIA/DASHBOARD/Dash1.png)


![Dashboard Image](https://github.com/saganash-21/ESP32-Cloud-Environment-Monitor/blob/main/MEDIA/DASHBOARD/Dash2.png)

---

## ✨ Features

- **Live Sensor Monitoring:** Tracks Temperature, Humidity, Sound Level (amplitude), and Ambient Light.  
- **Cloud Logging:** All data is logged and graphed on the Arduino IoT Cloud.  
- **Local Feedback System:**
  - 🔴 High Temp Alert: Red LED + dual-tone beep (controlled by an NPN transistor).  
  - 🟡 Low Light Warning: Yellow LED.  
  - 🔵 All Systems OK: Blue LED.  
  - ⚠️ Sensor Error: All three LEDs flash to indicate a sensor read failure.  
- **Remote Mute Switch:** Remotely silences the buzzer via the IoT Cloud dashboard.

---

## 🧰 Hardware Required

| Component              | Quantity |
| :----------------------| :-------: |
| ESP32 Development Board | 1 |
| DHT11 Sensor           | 1 |
| Sound Sensor Module    | 1 |
| LDR (Photoresistor)    | 1 |
| Red LED (5mm)          | 1 |
| Yellow LED (5mm)       | 1 |
| Blue LED (5mm)         | 1 |
| Passive Buzzer         | 1 |
| 220Ω Resistor          | 3 |
| 10kΩ Resistor          | 1 |
| Breadboard             | 1 |
| NPN Transistor (e.g. PN2222) | 1 |
| Jumper Wires           | As needed |

---

## ⚙️ Wiring Diagram

This project is built on a breadboard.  
Follow the connection table below or see the images in:  
[`/MEDIA/FEEDBACK/`](https://github.com/saganash-21/ESP32-Cloud-Environment-Monitor/tree/main/MEDIA/FEEDBACK)

| Component         | Signal Pin (to ESP32) | Power (3.3V) | Ground (GND) |
| :---------------- | :-------------------- | :------------ | :----------- |
| DHT11 Sensor       | GPIO14 | VCC | GND |
| Sound Sensor       | GPIO34 (A0) | VCC | GND |
| LDR (Photoresistor) | GPIO32 | VCC* | GND* |
| Red LED            | GPIO4 | - | via 220Ω resistor |
| Yellow LED         | GPIO18 | - | via 220Ω resistor |
| Blue LED           | GPIO5 | - | via 220Ω resistor |
| Passive Buzzer     | - | VCC | Collector of NPN |
| NPN Transistor     | Base → GPIO26 | - | Emitter → GND |

**LDR Circuit Note:**

- 3.3V → LDR Leg 1  
- LDR Leg 2 → GPIO32 **and** → 10kΩ resistor  
- Other end of 10kΩ resistor → GND  

**Transistor Circuit Note:**

- GPIO26 → 1kΩ resistor → Base of NPN  
- 3.3V → Buzzer Leg 1  
- Buzzer Leg 2 → Collector of NPN  
- Emitter → GND  

---

## ☁️ Software & Cloud Setup

### Arduino IoT Cloud

This project requires a free [Arduino IoT Cloud](https://cloud.arduino.cc/) account.

1. Log in and create a new **Thing**.  
2. Link your **ESP32** board.  
3. In the **Network** tab, enter your Wi-Fi credentials.  
4. In the **Setup** tab, create the following variables:

| Variable Name | Type | Permission |
| :------------- | :-------------------- | :----------- |
| temp | CloudTemperature | Read Only |
| humid | CloudRelativeHumidity | Read Only |
| light_level | int | Read Only |
| sound_level | int | Read Only |
| muteSwitch | bool | Read/Write |

5. After creation, download the generated `thingProperties.h` and `.ino` files.  
   Place them inside the [`/CODE/src/`](https://github.com/saganash-21/ESP32-Cloud-Environment-Monitor/tree/main/CODE/src) folder.

---

## 💻 Project Code

**File:** [`main.cpp`](https://github.com/saganash-21/ESP32-Cloud-Environment-Monitor/blob/main/CODE/src/main.cpp)  
**Author:** *Jeremy Ndirangu*  
**Date:** *28th October 2025*  

This sketch reads data from **DHT11**, **LDR**, and **Sound sensors**,  
sends it to the **Arduino IoT Cloud**, and controls **local feedback** (LEDs and buzzer)  
based on defined thresholds while filtering invalid DHT readings.

---

### 📂 Repository Structure

```
ESP32-Cloud-Environment-Monitor/
│
├── CODE/
│   └── src/
│       ├── main.cpp
│       └── thingProperties.h
│
├── MEDIA/
│   ├── DASHBOARD/
│   │   └── Dash1.png
│   │   └── Dash2.png
│   └── FEEDBACK/
│   │   └── blue.jpg
│   │   └── redBuzzer.mp4
│   │   └── yellow.mp4
│
└── CONNECTION/
    └── Wiring.pdf
```


---

## 🧠 Author

**Jeremy Ndirangu**  
Mechatronics Engineering Student | Embedded Systems Enthusiast  
[GitHub Profile](https://github.com/saganash-21)

---

## 🪪 License

This project is open source and available under the [MIT License](LICENSE).

---
