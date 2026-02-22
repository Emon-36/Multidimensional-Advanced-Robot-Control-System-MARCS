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

> **An autonomous heat-seeking guided rocket with onboard AI, dual-mode targeting, and a full Android Ground Control Station — built solo by a 3rd year EEE student.**

![Platform](https://img.shields.io/badge/Platform-ESP32-red?style=for-the-badge&logo=espressif)
![Language](https://img.shields.io/badge/Language-Kotlin%20%7C%20C%2B%2B-blue?style=for-the-badge&logo=kotlin)
![AI](https://img.shields.io/badge/AI-SSD%20MobileNet%20V2-orange?style=for-the-badge&logo=tensorflow)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)

---

## 🚀 What Is MARCS?

MARCS is not a hobby drone. It is a **two-phase autonomous guided rocket system** with:

- **Cruise Phase** → Waypoint-based GPS navigation
- **Terminal Phase** → Heat-seeking via custom photodiode array

Both phases run simultaneously with onboard AI classification for visual target verification.

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
│                ONBOARD SYSTEM                    │
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

### 🎯 Dual-Mode Targeting
| Mode | Technology | Range |
|------|-----------|-------|
| Passive IR | Custom 6x6 Photodiode Array | Up to 7m |
| Visual AI | SSD MobileNet V2 (Onboard) | Camera FOV |

### 📡 Ground Control Station
- **Live Map** with real-time GPS trajectory visualization
- **Waypoint Planning** with Dijkstra-based path optimization
- **Live Video Feed** with simultaneous object classification
- **Thermal Target Panel** with crosshair tracking
- **Mission Controls** — Start Mission / Simulation Mode
- **System Status** — Fuel, Signal, Obstacle Detection alerts

### 🔧 Hardware Innovation
- **Custom 6x6 Photodiode Array** — detects flame/heat up to 7m **without a transimpedance amplifier (TIA)** using spatial summation architecture
- **Dual ESP32 Architecture** — dedicated processors for vision and flight control
- **Canard Fin Actuation** — active aerodynamic guidance

### 🤖 Onboard AI
- SSD MobileNet V2 running inference **during flight**
- Real-time object classification streamed to GCS
- No cloud dependency — fully edge-deployed

---

## 📊 Sensor Fusion Pipeline

```
GPS Data ──────┐
               ├──► Kalman Filter ──► State Estimation ──► Guidance Law
BMP Altitude ──┤                                              │
               │                                              ▼
Thermal Data ──┘                                    Canard Actuation
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
| Target Acquisition | Custom Analog + SSD MobileNet V2 |

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

## 🎖 About The Builder

Built **solo** by **Md. Shahariar Khan Emon**
3rd Year EEE Student, University of Chittagong

- 📧 emon23702036@gmail.com
- 💼 [LinkedIn](https://linkedin.com/in/md-shahariar-khan-emon-8758a3327)
- 🐙 [GitHub](https://github.com/Emon-36)

---

> *"I don't just debug — I iterate. I don't just deploy — I optimize."*
