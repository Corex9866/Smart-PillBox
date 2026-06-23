# DoseMate Pro — Smart Pillbox Management System

> An IoT-powered medication management platform combining ESP32 hardware with a real-time web dashboard to improve medication adherence and simplify caregiving.

---

## Table of Contents
- [Overview](#overview)
- [Features](#features)
- [Technology Stack](#technology-stack)
- [System Architecture](#system-architecture)
- [Getting Started](#getting-started)
- [Workflow](#workflow)
- [Roadmap](#roadmap)
- [Contributing](#contributing)
- [License](#license)
- [Contributors](#contributors)

---

## Overview

DoseMate Pro is an end-to-end medication management system built for patients, elderly individuals, and caregivers who need reliable, real-time oversight of medication schedules. The system pairs a physical smart pillbox — powered by an ESP32 microcontroller and weight sensors — with a Firebase-backed web application, ensuring medication data stays synchronized and actionable across all devices.

The platform is designed around two core goals: **reducing missed doses** and **giving caregivers visibility without friction**.

---

## Features

- **Medication Scheduling** — Define dosage times, frequencies, and custom reminders through an intuitive web interface.
- **Smart Intake Monitoring** — Weight sensors detect whether a dose has been taken and log the event automatically.
- **Real-Time Sync** — All data flows through Firebase Firestore, keeping the dashboard and hardware in continuous sync.
- **Adherence Analytics** — Visual dashboards surface adherence trends over time to help identify patterns.
- **Low Inventory Alerts** — Automated alerts notify users when a compartment is running low on medication.
- **Caregiver & Emergency Contact Support** — Designate secondary contacts who receive alerts for missed doses or critical events.
- **Responsive Dashboard** — Fully responsive UI accessible from desktop and mobile browsers.
- **Offline-Capable Hardware** — Onboard buzzer and sensor modules handle local reminders and dose detection independently of network connectivity.

---

## Technology Stack

**Frontend**

| Technology | Purpose |
|---|---|
| React | Component-based UI framework |
| TypeScript | Type-safe application logic |
| Tailwind CSS | Utility-first responsive styling |

**Backend & Cloud**

| Technology | Purpose |
|---|---|
| Firebase Authentication | Secure user identity management |
| Firebase Firestore | Real-time NoSQL database for medication and adherence data |
| Firebase Hosting | Static web application deployment |

**Hardware**

| Component | Purpose |
|---|---|
| ESP32 Microcontroller | Core embedded controller — handles schedule retrieval, sensor polling, and reminders |
| HX711 + Load Cell Weight Sensors | Detects pill presence and estimates remaining inventory |
| Buzzer Module | Local audio reminders at scheduled dose times |

---

## System Architecture

```
┌─────────────────────────┐         ┌────────────────────────────┐
│      Web Dashboard      │◄───────►│     Firebase (Firestore)    │
│  React + TS + Tailwind  │         │  Auth / Hosting / Storage   │
└─────────────────────────┘         └──────────────┬───────────────┘
                                                     │
                                       Real-time sync (REST / WS)
                                                     │
                                      ┌──────────────▼───────────────┐
                                      │        ESP32 Firmware        │
                                      │  Schedule Retrieval          │
                                      │  Weight Sensor Polling       │
                                      │  Buzzer / Local Reminder     │
                                      └───────────────────────────────┘
```

---

## Getting Started

### Prerequisites
- Node.js v18+
- A Firebase project with Firestore and Authentication enabled
- Arduino IDE or PlatformIO (for ESP32 firmware)

### Web Application Setup
```bash
# Clone the repository
git clone https://github.com/Corex9866/Smart-PillBox.git
cd Smart-PillBox

# Install dependencies
npm install

# Configure Firebase
cp .env.example .env
# Add your Firebase project credentials to .env

# Start the development server
npm run dev
```

### ESP32 Firmware Setup
1. Open the `firmware/` directory in Arduino IDE or PlatformIO.
2. Update `config.h` with your Wi-Fi credentials and Firebase project details.
3. Flash the firmware to your ESP32 board.
4. Power on the device — it will connect to Firebase and begin polling for the active schedule.

---

## Workflow

1. **Schedule Creation** — The user adds medications and dose times through the web dashboard.
2. **Data Persistence** — Schedule data is written to Firebase Firestore.
3. **Hardware Polling** — The ESP32 retrieves the active schedule and monitors the pillbox at configured intervals.
4. **Dose Reminder** — At the scheduled time, the buzzer module triggers a local audio alert.
5. **Intake Detection** — Weight sensors detect a change in compartment load and log the dose as taken.
6. **Dashboard Update** — Adherence data updates in real time and is reflected in the analytics view.

---

## Future implementation

- [ ] Native mobile application (iOS & Android)
- [ ] SMS and WhatsApp notification support
- [ ] AI-based adherence prediction and risk alerts
- [ ] Voice assistant integration (Google Assistant / Alexa)
- [ ] Advanced health analytics and exportable reports
- [ ] Multi-user / multi-patient caregiver portal

---

## Contributing

Contributions are welcome. Please open an issue to discuss proposed changes before submitting a pull request.

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/your-feature`)
3. Commit your changes
4. Open a pull request

---

## License

This project is licensed under the [MIT License](LICENSE).

---

## Contributors

**Sairupesh BH**
B.Tech Computer Science & Engineering, VIT Chennai

---

*Built with ESP32, Firebase, and React as part of an IoT & Web Technologies initiative.*
