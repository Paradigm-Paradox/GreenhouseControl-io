# GreenhouseControl-io

[![Home Assistant Add-on](https://img.shields.io/badge/Home%20Assistant-Add--on-blue.svg)](https://www.home-assistant.io/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

**GreenhouseControl-io** is an autonomous, precision greenhouse automation add-on for Home Assistant. It orchestrates climate, VPD (Vapor Pressure Deficit), multi-zone smart irrigation, and supplemental lighting directly within your Home Assistant ecosystem.

---

## 🌟 Key Features

- **🌿 VPD-Driven Climate Automation**:
  - Automatically calculates real-time leaf and air VPD.
  - Controls exhaust fans, circulation fans, heaters, evaporative coolers, and misting systems to keep plants in optimal transpiration zones.
- **💧 Smart Irrigation & Safety Watchdogs**:
  - Moisture-triggered or schedule-based watering cycles.
  - Fail-safe runtime limits to eliminate the risk of accidental flooding.
  - Reservoir level monitoring and auto-shutoff.
- **☀️ Lighting & DLI (Daily Light Integral)**:
  - Tracks accumulated DLI from PAR/lux sensors.
  - Intelligently doses supplemental lighting to ensure maximum yields while cutting power waste.
- **🖥️ Ingress Web Dashboard**:
  - Embedded seamlessly inside your Home Assistant sidebar.
  - Live gauges, climate curves, zone controls, and manual actuator overrides.
- **🔗 Native Home Assistant Integration**:
  - Reads existing sensors and controls switches, valves, and dimmers without complex configuration.
  - MQTT discovery support for custom ESP32 / ESPHome greenhouse nodes.

---

## 📦 Installation via Home Assistant

1. In Home Assistant, navigate to **Settings** -> **Add-ons** -> **Add-on Store**.
2. Click the three dots (top-right) and select **Repositories**.
3. Add the repository URL:
   ```text
   https://github.com/Paradigm-Paradox/GreenhouseControl-io
   ```
4. Find **GreenhouseControl-io** in the add-on store list and click **Install**.
5. Configure your sensors and switches in the **Configuration** tab.
6. Click **Start** and select **Show in sidebar**.

---

## 🏗️ Architecture & Development

See [DESIGN.md](DESIGN.md) for detailed architectural blueprints, state machines, and calculations.

### Local Development / Testing
```bash
cd greenhouse_control
pip install -r requirements.txt
python -m uvicorn app.main:app --host 0.0.0.0 --port 8099 --reload
```

---

## 📄 License
This project is licensed under the MIT License.
