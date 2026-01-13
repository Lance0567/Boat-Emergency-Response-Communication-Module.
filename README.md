<div align="center">

  <h1>🚤 Boat Emergency Response System</h1>
  <h3>LoRa + GPS + GSM Communication Module</h3>

  <p>
    An embedded IoT prototype designed to improve maritime safety by detecting <br />
    emergency situations and transmitting real-time location data via long-range radio and SMS.
  </p>

  <p>
    <img src="https://img.shields.io/badge/Arduino-00979D?style=for-the-badge&logo=Arduino&logoColor=white" alt="Arduino" />
    <img src="https://img.shields.io/badge/C++-00599C?style=for-the-badge&logo=c%2B%2B&logoColor=white" alt="C++" />
    <img src="https://img.shields.io/badge/LoRa-Enabled-orange?style=for-the-badge&logo=rss&logoColor=white" alt="LoRa" />
    <img src="https://img.shields.io/badge/GPS-Tracking-blue?style=for-the-badge&logo=googlemaps&logoColor=white" alt="GPS" />
    <img src="https://img.shields.io/badge/GSM-Connectivity-green?style=for-the-badge&logo=whatsapp&logoColor=white" alt="GSM" />
  </p>

  </div>

<br />

## 📌 Overview

The **Boat Emergency Response System** is a failsafe communication module built for small vessels and fishing boats operating in areas with limited cellular coverage.

It continuously monitors water levels to detect sinking risks and allows for manual emergency triggering. When an emergency is detected, the system broadcasts the boat's exact GPS coordinates via **LoRa (Long Range Radio)** to a receiver station and simultaneously sends an **SMS alert** via GSM to registered responders.

---

## 🎯 Key Features

| Feature | Description |
| :--- | :--- |
| **📡 GPS Tracking** | Real-time acquisition of Latitude, Longitude, Date, and Time using the **NEO-6M** module. |
| **📶 LoRa Communication** | Long-range transmission (433 MHz) ensuring connectivity even without cellular signal. |
| **📩 GSM SMS Alerts** | Immediate text message notifications via **SIM800L** when a signal is available. |
| **🌊 Auto-Sinking Detection** | Water level sensors trigger an alarm automatically if water breaches a critical threshold. |
| **🔘 Manual SOS** | A physical panic button allowing the crew to instantly broadcast an emergency signal. |
| **🔄 Auto-Retry Logic** | The system re-attempts data transmission every minute until the emergency is cleared. |

---

## 🧠 System Architecture

### 1. The Sender Unit (Boat)
* **Controller:** Arduino Uno / Mega
* **Positioning:** NEO-6M GPS Module
* **Comms:** SX1278 LoRa (433MHz) + SIM800L GSM
* **Sensors:** Water Level Sensor + Push Button

### 2. The Receiver Unit (Shore/Rescue)
* **Controller:** Arduino / ESP32
* **Comms:** LoRa Receiver
* **Display:** Serial Monitor / LCD Dashboard

---

## 🔌 Hardware & Pin Configuration

> **Note:** Update the pin numbers below to match your specific wiring.

### 📍 LoRa SX1278 Connections
| LoRa Pin | Arduino Pin |
| :--- | :--- |
| VCC | 3.3V |
| GND | GND |
| SCK | D13 |
| MISO | D12 |
| MOSI | D11 |
| NSS (CS) | D10 |
| RST | D9 |
| DIO0 | D2 |

### 📍 GPS & GSM Connections
| Module | Module Pin | Arduino Pin |
| :--- | :--- | :--- |
| **GPS (NEO-6M)** | TX | D4 (SoftwareSerial RX) |
| | RX | D3 (SoftwareSerial TX) |
| **GSM (SIM800L)** | TX | D7 |
| | RX | D8 |
| **Sensors** | Water Sensor | A0 |
| | Button | D6 |

---

## 💻 Software & Libraries

To compile this project, install the following libraries in your **Arduino IDE**:

1.  **TinyGPS++** (by Mikal Hart) - For parsing NMEA GPS data.
2.  **LoRa** (by Sandeep Mistry) - For SPI communication with the SX1278.
3.  **SoftwareSerial** - For communicating with GPS/GSM modules on digital pins.

---

## 📤 Sample Output (Serial Monitor)

```text
[INIT] LoRa Initializing... OK!
[INIT] GPS Initializing... OK!
[STATUS] Monitoring Sensors...

>>> EMERGENCY TRIGGERED: Water Level High! <<<
[GPS] Fix Found!
[LORA] Sending Packet: "SOS,13.123456,123.654321,SINKING"
[GSM] Sending SMS to +63991xxxx... Sent!

[WAIT] Retrying in 60 seconds...
```

## 🚀 How to Run

1. **Hardware Setup:** Assemble the circuit following the pin configuration table above.
2. **Antennas:** Ensure external antennas for GPS, GSM, and LoRa are connected before powering on to prevent module damage.
3. **Power:** Use a stable 2A power source (SIM800L requires high current bursts).
4. **Upload:** Open the .ino file in Arduino IDE, select your board and port, and click Upload.
5. **Monitor:** Open Serial Monitor (Baud 9600) to view system logs.
