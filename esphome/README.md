# ESP32 Edge Nodes for GreenhouseControl-io

Greenhouse environments present unique hardware challenges: high humidity, temperature swings, metal framing that degrades RF signals, and moisture risks. 

**GreenhouseControl-io** leverages the **ESP32** microcontroller family (Wi-Fi, Ethernet, and Bluetooth BLE) as edge nodes that interface directly with physical sensors and high-voltage actuators.

---

## 🌟 Recommended ESP32 Hardware Profiles

| Node Profile | Recommended Board | Connectivity | Key Functions |
| :--- | :--- | :--- | :--- |
| **1. Canopy & Climate Node** | ESP32-WROOM-32 / ESP32-S3 | Wi-Fi (2.4 GHz) | Air Temp/RH (SHT40), Leaf IR Temp (MLX90614), CO2 (SCD40), Light/PAR (BH1750) |
| **2. Relay & Actuator Node** | WT32-ETH01 / Olimex ESP32-POE | **Ethernet (PoE / RJ45)** | High-voltage relays, 24VAC irrigation solenoids, vent louvers, 0-10V LED dimming |
| **3. Soil & Reservoir Node** | ESP32-DevKitC / ESP32-POE | Ethernet or Wi-Fi | RS485 Modbus NPK/EC probes, DS18B20 reservoir temp, ultrasonic tank level |
| **4. BLE Proxy Gateway** | ESP32-WROOM-32 | Wi-Fi + Bluetooth | Relays wireless plant sensors (MiFlora, Inkbird) directly into Home Assistant |

---

## ⚡ Why Ethernet ESP32 for Greenhouse Actuators?
Commercial and poly-tunnel greenhouses often feature galvanized steel arches, thermal foil, and dense wet plant canopies that attenuate 2.4 GHz Wi-Fi signals.
- For **relays and pumps**, we strongly advise **Ethernet-enabled ESP32 boards** (such as the **WT32-ETH01** or **Olimex ESP32-POE**).
- A wired Ethernet connection guarantees zero packet drops, eliminates Wi-Fi reconnect delays, and with PoE (Power over Ethernet), delivers power and data over a single waterproof CAT6 cable.

---

## 🛡️ Edge-Level Failsafes (Hardware Watchdogs)
All relay configurations in this directory include local hardware timers:
```yaml
switch:
  - platform: gpio
    name: "Irrigation Solenoid 1"
    pin: GPIO25
    id: relay_1
    # Hardware watchdog: Automatically turns off after 90 seconds
    # even if Home Assistant or the network completely disconnects!
    on_turn_on:
      - delay: 90s
      - switch.turn_off: relay_1
```
This guarantees that an irrigation valve or misting line can never accidentally stick open and flood your crop if a network glitch occurs.

---

## 🚀 Flashing & Quick Start
1. Install [ESPHome](https://esphome.io/) in Home Assistant or locally:
   ```bash
   pip install esphome
   ```
2. Plug your ESP32 into USB.
3. Compile and flash the desired template:
   ```bash
   esphome run canopy-node.yaml
   ```
4. Once flashed, Home Assistant will automatically notify you that a new ESPHome device was discovered!
