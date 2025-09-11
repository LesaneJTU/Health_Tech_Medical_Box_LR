# Health_Tech_Medical_Box_LR
This project is a real-time vital sign monitoring device powered by the Internet of Things. It combines a temperature sensor and a pulse sensor with Wi-Fi connectivity, enabling real-time data transfer to a web or mobile application. The project, which focuses on demonstrating IoT in healthcare monitoring, has been classified as "no problem related," indicating that it is primarily  exploratory and educational in nature. The project is still under development and improvement; it remains a work in progress.
---

## ✨ Features
- Real-time **heart rate monitoring** with a pulse sensor  
- Body **temperature measurement** via I²C temperature sensor  
- Visual feedback using a **16x2 I2C LCD display**  
- Serial monitor logging for debugging and data visualization  
- Configurable thresholds and LED blink feedback on pulse
---

## 🛠 Hardware Used
- **ESP32** development board  
- **Pulse Sensor** (analog input)  
- **MLX90614 IR Temperature Sensor** (I²C)  
- **16x2 LCD with I2C backpack**  
- **Breadboard + jumper wires**  
- (Optional) **LED for pulse blink feedback**  

---

## 📜 Software & Libraries
- **Arduino IDE** with ESP32 board support  
- Libraries:  
  - `LiquidCrystal_I2C` → LCD display  
  - `Wire.h` → I²C communication  
  - `PulseSensorPlayground` → Pulse sensor handling 
  - `Wifi` → Enables ESP32 to connect to a Wifi network  for real-time IoT data transmission
  - `HTTPClient` →   Allows the ESP32 to send HTTP requests, which is how data is uploaded to ThingSpeak and accessed by the app
  - `DFRobot_MLX90614` →  Used to interface with the MLX90614 infrared temperature sensor, making it easy to read accurate body temperature measurements

---
