## Health_Tech_Medical_Box_LR
This project is a real-time vital sign monitoring device powered by the Internet of Things. It combines a temperature sensor and a pulse sensor with Wi-Fi connectivity, enabling real-time data transfer to a web or mobile application. The project, which focuses on demonstrating IoT in healthcare monitoring, has been classified as "no problem related," indicating that it is primarily  exploratory and educational in nature. The project is still under development and improvement; it remains a work in progress.
---

##  Features
- Real-time **heart rate monitoring** with a pulse sensor  
- Body **temperature measurement** via I²C temperature sensor  
- Visual feedback using a **16x2 I2C LCD display**  
- Serial monitor logging for debugging and data visualization  
- Configurable thresholds and LED blink feedback on pulse
---

##  Hardware Used
- **ESP32** development board  
- **Pulse Sensor** (analog input)  
- **MLX90614 IR Temperature Sensor** (I²C)  
- **16x2 LCD with I2C backpack**  
- **Breadboard + jumper wires**  
- (Optional) **LED for pulse blink feedback**  

---

# Bill of Materials (BOM)

This table lists all the components required to build the ESP32 Pulse & Temperature Monitoring System.

| Component Name            | Purpose in Project                 | Quantity | Notes / Specifications        |
|----------------------------|------------------------------------|----------|--------------------------------|
| **ESP32**                 | Main microcontroller               | 1        | ESP32 DevKit V1 (recommended) |
| **Heart Rate Pulse Sensor**| Measure heart rate (BPM)           | 1        | Standard 3-pin pulse sensor   |
| **I²C LCD 16x2**           | Display all readings               | 1        | With I²C backpack for easy wiring |
| **IR Thermometer (MLX90614)** | Measures body temperature       | 1        | Object & ambient temperature sensing |
| **9V Battery**            | Powers the system                  | 1        | Rechargeable or disposable    |
| **9V Battery Snap Connector** | Connects battery to breadboard  | 1        | Male DC barrel jack optional  |
| **Jumper Wires**          | Electrical connections             | –        | Male-male + female-male assorted |
| **Breadboard**            | Circuit assembly & prototyping     | 1        | 400–830 tie-points recommended |

---

## Extras
- USB cable (for programming ESP32) 
- Small enclosure / 3D printed case for protection  

---

##  Software & Libraries
- **Arduino IDE** with ESP32 board support  
- Libraries:  
  - `LiquidCrystal_I2C` → LCD display  
  - `Wire.h` → I²C communication  
  - `PulseSensorPlayground` → Pulse sensor handling 
  - `Wifi` → Enables ESP32 to connect to a Wifi network  for real-time IoT data transmission
  - `HTTPClient` →   Allows the ESP32 to send HTTP requests, which is how data is uploaded to ThingSpeak and accessed by the app
  - `DFRobot_MLX90614` →  Used to interface with the MLX90614 infrared temperature sensor, making it easy to read accurate body temperature measurements

---

##  Circuit Connections
| Component             | ESP32 Pin   |
|-----------------------|-------------|
| Pulse Sensor (signal) | GPIO (PulseWire pin) |
| Pulse Sensor (VCC)    | 3.3V |
| Pulse Sensor (GND)    | GND |
| LCD (SDA)             | GPIO21 |
| LCD (SCL)             | GPIO22 |
| Temperature Sensor    | I²C bus (SDA/SCL shared) |

---

## Code Overview
- **`setup()`**: Initializes Serial, LCD, I²C, and pulse sensor  
- **`loop()`**: Reads pulse + temperature, updates LCD, and logs data

Example snippet:
```cpp
void setup() {
  Serial.begin(115200);
  Serial.println("Initializing ESP32 Health Monitor...");
  Serial.println("-----------------------------");

  // LCD Initialized
  lcd.init();
  lcd.clear();
  lcd.backlight();

  // Display startup message
  lcd.setCursor(0, 0);
  lcd.print("Pulse Monitor");
  lcd.setCursor(0, 1);
  lcd.print("Place finger");
}
```
---

## How the Code Works

### 1. Setup Phase (`setup()`)

- Initializes **Serial Monitor** for debugging.
- Sets up **LCD** and displays a startup message: `"Pulse Monitor - Place finger"`.
- Configures the **pulse sensor** (input pin, LED blink, threshold).
- Initializes the **temperature sensor** (MLX90614).
- Connects the ESP32 to **Wi-Fi**.
- Starts a lightweight **web server** on port 80.

### 2. Main Loop (`loop()`)

- Reconnects Wi-Fi if the connection drops.
- Reads pulse data, calculates **BPM**, and determines pulse status (`Low`, `Normal`, `High Pulse`).
- Reads **ambient** and **object temperature** every second.
- Logs all readings to **Serial Monitor**.
- Sends data periodically to **ThingSpeak**.
- Handles **HTTP client requests** for live data on the ESP32-hosted web page.

### 3. Web Dashboard (`handleClientRequest()`)

- Serves a **responsive HTML page** with:
  - Heartbeat animation ♥ when pulse is detected
  - BPM, signal strength, and last beat time
  - Object and ambient temperature readings
  - Wi-Fi and ThingSpeak connection status
- Auto-refreshes every 5 seconds for real-time updates.

### 4. ThingSpeak Integration (`sendToThingSpeak()`)

- Formats sensor data into a ThingSpeak API URL.
- Sends via HTTP GET request.
- Confirms success or logs errors.

---
## Project Pictures

### Schematic
<img width="1126" height="478" alt="Schematic" src="https://github.com/user-attachments/assets/dca02ac0-5094-4a9f-abc3-c77fdd588a01" />
### Sketch of Components Connected 
<img width="777" height="596" alt="sketch of components" src="https://github.com/user-attachments/assets/0cd73437-945a-441a-bf9c-ee423894ca58" />
### Physical Board Setup
<img width="1125" height="624" alt="Screenshot 2025-09-12 091336" src="https://github.com/user-attachments/assets/85eb5a3c-8d8e-4db6-94f8-6acac3266523" />
### Components
<img width="1316" height="726" alt="Screenshot 2025-09-12 091256" src="https://github.com/user-attachments/assets/71c44f3b-7e62-4335-8607-553b31c6c989" />
### Components Wires
<img width="1347" height="747" alt="Screenshot 2025-09-12 091007" src="https://github.com/user-attachments/assets/181cb9d5-b1e7-4268-beda-c500424a766b" />
### ThingSpeak Live Feed
<img width="1249" height="786" alt="Screenshot 2025-09-12 090642" src="https://github.com/user-attachments/assets/b2adc76e-624c-4b37-8c53-6d7bce9c27c8" />
### MIT App
![Uploading IMG_0021.jpeg…]()

### Pulse Sensor Reading


