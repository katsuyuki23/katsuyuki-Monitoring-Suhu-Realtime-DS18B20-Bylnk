# katsuyuki-Monitoring-Suhu-Realtime-DS18B20-Bylnk
IoT-based temperature monitoring system that utilizes the DS18B20 sensor as a source of high-precision thermal data. Temperature data is sent in real time via a WiFi connection to the Blynk platform, enabling temperature visualization, logging and automatic notifications.

🔧 Components & Preparation

DS18B20 (waterproof or non-waterproof) + 4.7 kΩ resistor as pull-up.

ESP8266 / ESP32 boards.

Jumper cables, breadboard (optional).

Arduino IDE + libraries: OneWire.h, DallasTemperature.h, and Blynk libraries (e.g. BlynkSimpleEsp8266.h or BlynkSimpleEsp32.h) 

Blynk account & configuration: create a new project in Blynk → get an Auth Token — it will be inserted into the code. 

DS18B20 Wiring → ESP:

DS18B20 pins ESP pins
VCC 3.3 V (or 5 V depending on board)
GND GND
Data of one of the digital GPIOs (example D4 on ESP8266) + pull-up to VCC with 4.7 kΩ resistor

| DS18B20 pins | ESP pins |
| ----------- | -------------------------------------------------------------------------------------------------------------- |
| VCC | 3.3 V (or 5 V depending on board) |
| GND | GND |
| Data | one digital GPIO (example D4 on ESP8266) + pull-up to VCC with 4.7 kΩ resistor ([mjrobot.org][1]) |

⚙️ Set-up in Blynk App

Open Blynk → create a new project with a suitable board (ESP8266/ESP32) + WiFi connection. 

Get Auth Token, then enter it in the code.

Add widget (Gauge / Value) → connect to Virtual Pin V0 (or another pin according to the code).

Run the project (tap “Play”) → if the hardware & connection is correct → the temperature will appear in real-time.

📈 Explanation & Tips

DS18B20 uses 1-Wire protocol → allows multiple sensors on one data path (if more than one sensor is needed). 

Accuracy: −55°C to +125°C, up to 12-bit resolution → ±0.5°C accurate within normal range. 

The data reading & sending interval can be adjusted (for example every 1 second as in the code).

If WiFi or Blynk connection is lost → temperature data will fail to send — ensure stable connection / error responsibility.

🔄 Adaptations & Extensions

Can use ESP32 (replace BlynkSimpleEsp8266.h with BlynkSimpleEsp32.h + DS18B20 pin according to the board).

Add logging (for example to SD-card / database) or threshold alert: send notification via Blynk when the temperature exceeds the limit.

Can be combined with other sensors (humidity, light, etc.) for complete environmental monitoring.
