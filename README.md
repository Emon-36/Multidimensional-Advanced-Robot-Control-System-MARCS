# ⚡ MARCS
### Multidimensional Advanced Robot Control System

```
    ███╗   ███╗ █████╗ ██████╗  ██████╗███████╗
    ████╗ ████║██╔══██╗██╔══██╗██╔════╝██╔════╝
    ██╔████╔██║███████║██████╔╝██║     ███████╗
    ██║╚██╔╝██║██╔══██║██╔══██╗██║     ╚════██║
    ██║ ╚═╝ ██║██║  ██║██║  ██║╚██████╗███████║
    ╚═╝     ╚═╝╚═╝  ╚═╝╚═╝  ╚═╝ ╚═════╝╚══════╝
```

> **A canard-based autonomous flight control system with onboard AI, dual-mode target acquisition, and a full Android Ground Control Station — built solo by a 3rd year EEE student.**

![Platform](https://img.shields.io/badge/Platform-ESP32-red?style=for-the-badge&logo=espressif)
![Language](https://img.shields.io/badge/Language-Kotlin%20%7C%20C%2B%2B-blue?style=for-the-badge&logo=kotlin)
![AI](https://img.shields.io/badge/AI-SSD%20MobileNet%20V2-orange?style=for-the-badge&logo=tensorflow)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)

---

## 🚀 What Is MARCS?

MARCS is a **canard-based flight control system** designed for guided aerial vehicles. It handles active aerodynamic control through canard fin actuation, sensor fusion, and dual-mode target acquisition — with a companion Android GCS for mission oversight.

**Two-phase guidance logic:**
- **Cruise Phase** → Waypoint-based GPS autonomous navigation
- **Terminal Phase** → Heat-seeking via custom photodiode array

---

## 🧠 System Architecture

```
┌─────────────────────────────────────────────────┐
│                  ANDROID GCS                     │
│  ┌──────────┐  ┌──────────┐  ┌───────────────┐  │
│  │ Live Map │  │ Telemetry│  │ Vision Feed   │  │
│  │ Waypoint │  │ GPS/Alt  │  │ Object Class. │  │
│  │ Planning │  │ Speed/Fuel│  │ Thermal Target│  │
│  └──────────┘  └──────────┘  └───────────────┘  │
└────────────────────┬────────────────────────────┘
                     │ LoRa / WiFi
┌────────────────────▼────────────────────────────┐
│              FLIGHT CONTROL SYSTEM               │
│                                                  │
│  ┌─────────────────┐    ┌──────────────────────┐ │
│  │   ESP32-CAM      │    │      ESP32           │ │
│  │                 │    │                      │ │
│  │ SSD MobileNet V2│    │ Kalman Filter Fusion │ │
│  │ Live Inference  │    │ PID/PN Guidance      │ │
│  │ Object Class.   │    │ Canard Actuation     │ │
│  └─────────────────┘    │ GPS + BMP + Thermal  │ │
│                         └──────────────────────┘ │
│                                                  │
│  ┌──────────────────────────────────────────────┐│
│  │        6x6 Photodiode Array (Custom)         ││
│  │     Heat Seeking • 7m Range • No TIA         ││
│  └──────────────────────────────────────────────┘│
└─────────────────────────────────────────────────┘
```

---

## ✨ Key Features

### 🎯 Dual-Mode Target Acquisition
| Mode | Technology | Range |
|------|-----------|-------|
| Passive IR | Custom 6x6 Photodiode Array | Up to 7m |
| Visual AI | SSD MobileNet V2 (Onboard) | Camera FOV |

### 📡 Ground Control Station (Android)
- **Live Map** with real-time GPS trajectory visualization
- **Waypoint Planning** with Dijkstra-based path optimization
- **Live Video Feed** with simultaneous object classification
- **Thermal Target Panel** with crosshair tracking
- **Mission Controls** — Start Mission / Simulation Mode
- **System Status** — Fuel, Signal, Obstacle Detection alerts

### 🔧 Hardware
- **Canard Fin Actuation** — active aerodynamic control
- **Custom 6x6 Photodiode Array** — detects heat up to 7m **without a transimpedance amplifier (TIA)**, using spatial summation architecture
- **Dual ESP32 Architecture** — dedicated processors for vision and flight control

### 🤖 Onboard AI
- SSD MobileNet V2 running **on-device inference**
- Real-time object classification streamed to GCS
- Fully edge-deployed — no cloud dependency

---

## 📊 Sensor Fusion Pipeline

```
GPS Data ──────┐
               ├──► Kalman Filter ──► State Estimation ──► Guidance Law
BMP Altitude ──┤                                              │
               │                                              ▼
Thermal Data ──┘                                      Canard Actuation
                                                    (PID / PN Guidance)
```

---

## 🛠 Tech Stack

| Layer | Technology |
|-------|-----------|
| GCS App | Kotlin, Jetpack Compose |
| Onboard Vision | Embedded C++, TFLite |
| Communication | LoRa, WiFi |
| Navigation | GPS, Dijkstra Algorithm |
| Sensor Fusion | Kalman Filter |
| Guidance | PID / Proportional Navigation |
| Target Acquisition | Custom Analog Array + SSD MobileNet V2 |

---

## 🗂 Repository Structure

```
MARCS/
├── app/                    # Android GCS Application
│   ├── ui/                 # Jetpack Compose Screens
│   │   ├── Dashboard       # Main telemetry view
│   │   ├── MapView         # GPS trajectory + waypoints
│   │   ├── LiveFeed        # Camera + AI classification
│   │   └── MissionControl  # Start/Stop/Simulation
│   └── data/               # Telemetry data models
├── firmware/               # ESP32 Embedded C++ (coming)
└── docs/                   # Architecture documentation
```

---

## ⚠️ Project Status

| Component | Status |
|-----------|--------|
| Android GCS | ✅ Complete |
| Canard Actuation | ✅ Complete |
| Photodiode Array | ✅ Complete |
| Onboard AI (SSD MobileNet V2) | ✅ Complete |
| Kalman Filter Fusion | ✅ Complete |
| Waypoint Navigation | ✅ Complete |
| Firmware (open source) | 🔄 Coming Soon |

---

## 🎖 About The Builder

Built **solo** by **Md. Shahariar Khan Emon**
3rd Year EEE Student, University of Chittagong

- 📧 emon23702036@gmail.com
- 💼 [LinkedIn](https://linkedin.com/in/md-shahariar-khan-emon-8758a3327)
- 🐙 [GitHub](https://github.com/Emon-36)

---
