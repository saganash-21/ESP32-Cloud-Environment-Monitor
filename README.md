#ESP32 ENVIRONMENTAL MONITOR WITH ARDUINO IoT CLOUD

This project uses an ESP32 to monitor a room's environment in real-time. It tracks temperature, humidity, light, and sound levels, and sends the data to the Arduino IoT Cloud for a live, interactive dashboard. The system also provides local visual (LED) and audible (buzzer) alerts for high temperatures or low light.

📈 Live Dashboard

The dashboard provides a live view of all sensors, as well as historical data in charts. It also features a "Mute" switch to remotely silence the on-device buzzer.
The live dashboard images can be found in the MEDIA/DASHBOARD/ folder.

✨ Features

Live Sensor Monitoring: Tracks Temperature, Humidity, Sound Level (amplitude), and Ambient Light.
Cloud Logging: All data is logged and graphed on the Arduino IoT Cloud.
Local Feedback System:
    High Temp Alert: Red LED + dual-tone beep(controlled by an NPN transistor).
    Low Light Warning: Yellow LED.
    All Systems OK: Blue LED.
    Sensor Error: All three LEDs flash to indicate a sensor read failure.
Remote Mute Switch: A switch on the dashboard can remotely silence the buzzer.

---
1. Hardware Required

|         Component        | Quantity |
| :----------------------- | :------- |
| ESP32 Development Board  |    1     |
| DHT11 Sensor             |    1     |
| Sound Sensor Module      |    1     |
| LDR (Photoresistor)      |    1     |
| Red LED (5mm)            |    1     |
| Yellow LED (5mm)         |    1     |
| Blue LED (5mm)           |    1     |
| Passive Buzzer           |    1     |
| 220&Omega; Resistor      |    3     |
| 10k&Omega; Resistor      |    1     |
| Breadboard               |    1     |
| NPN transistor           |    1     |
| Jumper Wires             |As needed |
|                          |          |
---

2. Wiring Diagram

This project is built on a breadboard. Follow the connection table the file path:\CONNECTION\Wiring.
You can also find images of the physical connection in the following file path:\MEDIA\FEEDBACK\
|  COMPONENT         | SIGNAL PIN(to ESP32) |  POWER PIN(3.3V) |  GROUND PIN(TO GND) |
| :----------------- | :------------------- | :--------------- | :------------------ |
| DHT11 Sensor       |       GPIO14         |       VCC        |         GND         |
| Sound Sensor       |       GPIO34(A0)     |       VCC        |         GND         |
| LDR(Photoresistor) |       GPIO32         |       VCC*       |         GND*        |
| Red LED            |       GPIO4          |        -         |   via 220 resistor  |
| Yellow LED         |       GPIO18         |        -         |   via 220 resistor  | 
| Blue LED           |       GPIO5          |        -         |   via 220 resistor  |
| Passive Buzzer     |         -            |       VCC        |   collector of NPN  |
| NPN Transistor     |   GPIO26 --> BASE    |        -         |   EMMITER --> GND   |

 *Note on LDR: The LDR is in a voltage divider circuit.

 Connect 3.3V to one leg of the LDR.
 
 Connect the other leg of the LDR to both GPIO 32 (the signal pin) AND one leg of a 10kΩ resistor.
 
 Connect the other leg of the 10kΩ resistor to GND.
 
 
 *Note on the transistor
 
 GPIO 26 → 1kΩ Resistor → Base of NPN Transistor
 
 3.3V → Buzzer Leg 1
 
 Buzzer Leg 2 → Collector of NPN Transistor
 
 Emitter of NPN Transistor → GND




3. Software & Cloud Setup

Arduino IoT Cloud

This project requires a free Arduino IoT Cloud account.

1.  Log in to the Arduino IoT Cloud and create a new "Thing".
2.  Link your ESP32 board.
3.  Go to the "Network" tab and enter your Wi-Fi credentials.
4.  Go to the "Setup" tab and create the following 5 variables:

| Variable Name | Type                  | Permission  |
| :------------ | :-------------------- | :---------- |
|  temp         | CloudTemperature      |  Read Only  |
|  humid        | CloudRelativeHumidity |  Read Only  |
|  light_level  | int                   |  Read Only  |
|  sound_level  | int                   |  Read Only  |
|  muteSwitch   | bool                  | Read/Write  |

5.  After creating these, the cloud will provide you with a `thingProperties.h` file and a skeleton `.ino` file. Download them and place them in the `/CODE/src` folder.

Project Code

This is the complete and final code for the main `.ino` file. It includes the logic to prevent `NaN` errors from the DHT sensor, which keeps the graphs clean and reliable.



 Project: ESP32 Environmental Monitor

 Author: Jeremy Ndirangu

 Date: 28th October 2025 

 This sketch reads data from DHT11, LDR, and Sound sensors,

 sends it to the Arduino IoT Cloud, and controls local feedback

 (LEDs and a buzzer) based on sensor thresholds.


Code: \CODE\src\main.cpp





