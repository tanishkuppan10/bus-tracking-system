# 🚍 Smart Bus Tracker — Real-Time School Bus Tracking System

<p align="center">
  <img src="https://img.shields.io/badge/Platform-Android-green?style=for-the-badge&logo=android" />
  <img src="https://img.shields.io/badge/Language-Java-orange?style=for-the-badge&logo=java" />
  <img src="https://img.shields.io/badge/Maps-OpenStreetMap-blue?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Min%20SDK-24-brightgreen?style=for-the-badge" />
  <img src="https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge" />
</p>

<p align="center">
  <b>A smart, real-time GPS-based bus tracking system for students and drivers — built with Android (Java), OpenStreetMap, and Material Design.</b>
</p>

---

## 📌 About The Project

**Smart Bus Tracker** is an Android application designed to improve the **safety and convenience** of students who commute via school/college buses. Inspired by systems like Telangana's school bus tracking model, this app provides **live GPS tracking**, **ETA calculation**, **driver contact access**, and **seat availability** — all within a clean, modern Material Design interface.

The app supports **two roles** in a single APK:

| 🎓 Student Mode | 🚌 Driver Mode |
|---|---|
| Enter bus code to find a bus | Toggle GPS tracking ON/OFF |
| View live bus location on map | Update available seat count |
| See real-time ETA & distance | View current GPS coordinates |
| Call the driver with one tap | See map preview of location |
| Browse all available buses | Control bus active status |

> **No API key required!** The app uses **OpenStreetMap (OSMDroid)** for maps — completely free and open source.

---

## 🎯 Problem Statement

Students face daily challenges while commuting via school/college buses:
- ❌ No visibility on bus location or estimated arrival time
- ❌ Difficulty contacting the driver during emergencies
- ❌ No way to know if seats are available
- ❌ Safety concerns for parents and institutions

**Smart Bus Tracker** solves all of these by providing a **real-time tracking platform** that connects students and drivers.

---

## ✨ Key Features

### 🔐 Authentication System
- Email & password based login/registration
- Role-based access (Student / Driver)
- Persistent session management using SharedPreferences
- Pre-loaded demo accounts for easy testing

### 📍 Live GPS Tracking
- Real-time bus location displayed on **OpenStreetMap**
- Bus marker updates every **3 seconds**
- Student's own location shown on map
- One-tap button to center the map on the bus
- Proximity alerts when bus is within **500 meters**

### ⏱️ ETA Calculation
- Calculates distance using the **Haversine formula**
- Estimates arrival time based on average bus speed (30 km/h)
- Dynamically updates as the bus moves
- Shows formatted distance (meters/kilometers)

### 👨‍✈️ Driver Contact
- Driver name and phone number displayed prominently
- **One-tap "Call Driver"** button opens the phone dialer
- Available from both dashboard and map screen

### 💺 Seat Availability
- Real-time seat count (available / total)
- Driver can increase or decrease count manually
- Students can see availability before boarding

### 🔔 Proximity Alerts
- Automatic notification when bus is within 500m
- Visual indicator on the tracking screen
- Helps students prepare for boarding

### 🚌 Multi-Bus Support
- **10 pre-loaded buses** (BUS101 – BUS110)
- Each with unique route, driver, and GPS coordinates
- Simulated movement along Hyderabad routes
- Browse all buses in a scrollable list

---

## 🏗️ System Architecture

```
┌─────────────────────────────────────────────────┐
│              Smart Bus Tracker App               │
│                                                  │
│    ┌──────────────┐     ┌──────────────────┐    │
│    │  Student App  │     │    Driver App     │    │
│    │              │     │                  │    │
│    │ • Search Bus │     │ • Toggle GPS     │    │
│    │ • View Map   │     │ • Update Seats   │    │
│    │ • See ETA    │     │ • View Location  │    │
│    │ • Call Driver│     │ • Map Preview    │    │
│    └──────┬───────┘     └────────┬─────────┘    │
│           │                      │               │
│    ┌──────┴──────────────────────┴──────────┐   │
│    │         In-Memory Data Store            │   │
│    │  (Singleton - replaces Firebase)        │   │
│    │                                         │   │
│    │  • 10 Buses with GPS coordinates        │   │
│    │  • User accounts & authentication       │   │
│    │  • Real-time listener pattern           │   │
│    └──────────────┬──────────────────────────┘   │
│                   │                              │
│    ┌──────────────┴──────────────────────────┐   │
│    │          Bus Simulator                   │   │
│    │  Moves buses along predefined routes     │   │
│    │  every 3 seconds (Hyderabad waypoints)   │   │
│    └─────────────────────────────────────────┘   │
└─────────────────────────────────────────────────┘
```

---

## 🛠️ Tech Stack

| Technology | Purpose |
|---|---|
| **Java** | Primary programming language |
| **Android SDK 34** | Target platform (Min SDK 24) |
| **OSMDroid 6.1.18** | OpenStreetMap integration (no API key) |
| **Material Design** | Modern UI components |
| **Google Play Services Location** | GPS/Location services |
| **SharedPreferences** | Session persistence |
| **RecyclerView + CardView** | Scrollable bus list with cards |
| **Handler/Runnable** | Real-time update mechanism |

---

## 📁 Project Structure

```
SmartBusTracker/
├── app/src/main/
│   ├── java/com/smartbus/tracker/
│   │   ├── activities/
│   │   │   ├── SplashActivity.java          # Animated splash screen
│   │   │   ├── LoginActivity.java           # Login with role tabs
│   │   │   ├── RegisterActivity.java        # New user registration
│   │   │   ├── StudentDashboardActivity.java# Student main screen
│   │   │   ├── BusTrackingActivity.java     # Live map tracking
│   │   │   ├── DriverDashboardActivity.java # Driver controls
│   │   │   └── SettingsActivity.java        # Profile & logout
│   │   ├── adapters/
│   │   │   └── BusListAdapter.java          # Bus list RecyclerView
│   │   ├── models/
│   │   │   ├── Bus.java                     # Bus data model
│   │   │   └── User.java                    # User data model
│   │   └── utils/
│   │       ├── BusSimulator.java            # GPS movement simulation
│   │       ├── Constants.java               # App constants
│   │       ├── DataStore.java               # In-memory database
│   │       ├── ETACalculator.java           # Distance & ETA math
│   │       └── SessionManager.java          # Login session handler
│   ├── res/
│   │   ├── layout/                          # 8 XML layouts
│   │   ├── drawable/                        # 10 drawable resources
│   │   └── values/                          # Colors, strings, themes
│   └── AndroidManifest.xml
├── build.gradle
├── settings.gradle
└── README.md
```

---

## 🚀 Getting Started

### Prerequisites
- **Android Studio** (Arctic Fox or later recommended)
- **JDK 11** or higher
- Android Emulator or physical device (API 24+)

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/YOUR_USERNAME/SmartBusTracker.git
   ```

2. **Open in Android Studio**
   - File → Open → Select the `SmartBusTracker` folder
   - Wait for Gradle sync to complete

3. **Run the app**
   - Select an emulator or connected device
   - Click ▶️ Run

> ⚠️ **No additional setup needed!** No API keys, no Firebase config, no backend server.

### Demo Credentials

| Role | Email | Password |
|------|-------|----------|
| 🎓 Student | `student@demo.com` | `123456` |
| 🚌 Driver | `driver@demo.com` | `123456` |

---

## 📱 App Screens

| Screen | Description |
|--------|-------------|
| **Splash** | Animated logo with gradient background |
| **Login** | Student/Driver tab toggle, email/password |
| **Register** | Full registration with role & bus code selection |
| **Student Dashboard** | Bus code search, info card, ETA, call driver |
| **Bus Tracking** | Full-screen map with live bus movement |
| **Driver Dashboard** | GPS toggle, seat management, coordinates |
| **Settings** | Profile info and logout |

---

## 🗺️ Pre-loaded Bus Data

The app comes with **10 demo buses** pre-configured with Hyderabad (India) coordinates:

| Bus Code | Route | Driver | Seats |
|----------|-------|--------|-------|
| BUS101 | Route A — Kukatpally to Campus | Ramesh Kumar | 40 |
| BUS102 | Route B — Secunderabad to Campus | Suresh Reddy | 40 |
| BUS103 | Route C — Gachibowli to Campus | Venkat Rao | 40 |
| BUS104 | Route D — Dilsukhnagar to Campus | Mahesh Singh | 40 |
| BUS105 | Route E — Ameerpet to Campus | Ashok Sharma | 40 |
| BUS106 | Route F — ECIL to Campus | Rajesh Verma | 40 |
| BUS107 | Route G — LB Nagar to Campus | Srinivas Goud | 40 |
| BUS108 | Route H — Miyapur to Campus | Praveen Kumar | 40 |
| BUS109 | Route I — Uppal to Campus | Naveen Reddy | 40 |
| BUS110 | Route J — Mehdipatnam to Campus | Kiran Prasad | 40 |

All buses simulate movement along their routes automatically.

---

## 🧮 How ETA Works

The app uses the **Haversine Formula** to calculate the great-circle distance between the student's GPS location and the bus's GPS location:

```
a = sin²(Δlat/2) + cos(lat1) × cos(lat2) × sin²(Δlng/2)
c = 2 × atan2(√a, √(1−a))
distance = R × c    (where R = 6371 km)
```

ETA is then estimated using:
```
ETA = distance / average_speed    (default: 30 km/h)
```

---

## 🔮 Future Enhancements

- [ ] Firebase Realtime Database integration for production use
- [ ] Google Maps API support (optional)
- [ ] Push notifications via Firebase Cloud Messaging
- [ ] Live route polyline on map
- [ ] Multiple bus stops with stop-by-stop tracking
- [ ] Parent tracking access
- [ ] SOS / Panic button for emergencies
- [ ] Student attendance system (check-in/check-out)
- [ ] Admin panel for school authorities
- [ ] Dark mode support

---

## 🤝 Contributing

Contributions are welcome! Feel free to:

1. Fork the project
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📄 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

---

## 👨‍💻 Author

**Your Name**

- GitHub: [@YOUR_USERNAME](https://github.com/YOUR_USERNAME)

---

## ⭐ Show Your Support

If this project helped you, give it a ⭐ on GitHub!

---

<p align="center">
  Made with ❤️ for smarter, safer student commutes
</p>
