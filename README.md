# 🌡️ **katsuyuki — Monitoring Suhu Realtime DS18B20 + Blynk**

Sistem IoT untuk memantau suhu secara realtime menggunakan sensor **DS18B20** dan pengiriman data melalui **WiFi** ke platform **Blynk**. Menyediakan visualisasi suhu, logging, dan notifikasi otomatis.

---

## 🚀 **Fitur Utama**

* Monitoring suhu realtime lewat Blynk Dashboard (Mobile/Web).
* Sensor **DS18B20** dengan akurasi tinggi (±0.5°C).
* Kompatibel dengan **ESP8266** & **ESP32**.
* Bisa diperluas: logging, alarm suhu, multi-sensor.

---

## 🔧 **Hardware yang Dibutuhkan**

* ESP8266 / ESP32.
* Sensor DS18B20 (waterproof/non‑waterproof).
* Resistor 4.7 kΩ (pull‑up).
* Jumper wires.
* Breadboard (opsional).

---

## 🔌 **Wiring DS18B20 → ESP**

| DS18B20 | ESP                      | Catatan                           |
| ------- | ------------------------ | --------------------------------- |
| VCC     | 3.3V / 5V                | Sesuai board                      |
| GND     | GND                      | —                                 |
| DATA    | GPIO (contoh D4 ESP8266) | Wajib pakai pull‑up 4.7 kΩ ke VCC |

```
DS18B20 DATA ---[4.7kΩ]--- VCC
```

---

## 📲 **Setup di Blynk (IoT Platform)**

1. Buat **Template baru** → pilih board (ESP8266/ESP32).
2. Masukkan WiFi + Auth Token (didapat dari Blynk).
3. Buat **Datastream Virtual Pin V0** (type: Double / Numeric).
4. Tambahkan widget **Gauge** → hubungkan ke `V0`.
5. Save & Run.

---

## 🧠 **Penjelasan Singkat**

* DS18B20 memakai protokol **1‑Wire** → satu pin data bisa untuk banyak sensor.
* Pembacaan suhu → diproses ESP → dikirim ke Blynk via `virtualWrite(V0, nilaiSuhu)`.
* Refresh data default: setiap 1 detik.
* Stabilitas koneksi WiFi sangat berpengaruh.

---

## 🧩 **Kode Contoh (Minimalist & Clean)**

```cpp
#include <OneWire.h>
#include <DallasTemperature.h>
#include <WiFi.h>
#include <BlynkSimpleEsp32.h>
// ESP8266: gunakan BlynkSimpleEsp8266.h

char auth[] = "BLYNK_TOKEN";
char ssid[] = "WIFI_SSID";
char pass[] = "WIFI_PASS";

#define ONE_WIRE_BUS 4 // GPIO4 / D4
OneWire oneWire(ONE_WIRE_BUS);
DallasTemperature sensors(&oneWire);

BlynkTimer timer;

void sendTemp() {
    sensors.requestTemperatures();
    float t = sensors.getTempCByIndex(0);
    Blynk.virtualWrite(V0, t);
}

void setup() {
    Serial.begin(115200);
    sensors.begin();
    Blynk.begin(auth, ssid, pass);
    timer.setInterval(1000L, sendTemp);
}

void loop() {
    Blynk.run();
    timer.run();
}
```

---

## 📈 **Troubleshooting Cepat**

* Gauge tidak bergerak → cek datastream harus `V0`.
* Nilai `-127°C` → sensor tidak terbaca / wiring salah.
* Nilai freeze → WiFi drop / perangkat offline.
* Jangan pakai `delay()` besar → gunakan `BlynkTimer`.

---

## 🔮 **Pengembangan Lanjutan**

* Multi-sensor DS18B20 dalam satu pin data.
* Alarm suhu → Push Notification Blynk.
* Logging ke database (InfluxDB / Firebase).
* Integrasi dashboard grafis (Grafana / Blynk Chart).

---

## 🏁 **Status Proyek**

Aktif & dapat diperluas sesuai kebutuhan.

---

## 👤 **Author**

**katsuyuki — IoT Implementation & Monitoring System**

---

dipublish sebagai README proyek GitHub.
