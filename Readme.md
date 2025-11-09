# Checkpoint-System
**Real-time Timing & Checkpoint Tracking System for Robotics Competitions**

## Overview

**Checkpoint-System** is a complete Embedded + Web timing solution designed for autonomous racing robots.  
The system records the precise timestamp whenever a robot passes a checkpoint, calculates segment travel time, and displays real-time race progress on a web dashboard.

This project was developed for **ROBOCUS 2024** – Robotics Research & IoT Laboratory, University of Science (HCMUS), Ho Chi Minh City.

This project aims to support performance evaluation, racing logic tracking, and transparent progress display during competitions.

---

## Key Features
- Detects and logs robot arrival times at multiple checkpoints
- Calculates intermediate time between checkpoints
- Sends timing data to a local server via WiFi (using WebSocket protocol)
- Web dashboard visualizes robot progress, timing history, and stats in real-time
- Expandable architecture for additional checkpoints or robot IDs

---

## Hardware
- **Microcontroller board:** ESP32
- **Communication interfaces:** WiFi
- **Sensors:** E3F-DS30Y1 AC SCR Adjustable IR Infrared Proximity Sensor for checkpoint detection
- **Power:** 5V regulated supply for sensors and MCU
- **Configurable firmware data structures** for multiple robots and checkpoints

---

## System Architecture
```
[Sensors] → [ESP32 MCU] → [WebSocket Client] → [WebSocket Server] → [Database] → [Web Dashboard (UI)]
```

## Use Cases
- **Time-tracking for autonomous robotics competitions:** accurately measure robot lap times
- **Checkpoint-based racing systems:** ensure robots pass checkpoints in the correct order
- **Real-time performance analytics for IoT robots:** monitor speed, segment time, and progress live on dashboard

## Project Structure
```
    Checkpoint-System/
    │
    ├── Checkpoint_System/ # Embedded code for ESP32 (sensor reading + WebSocket communication)
    ├── checkpoint-web/ # Web dashboard
    └── README.md
```

## Features
- Interrupt-based detection of IR sensors at checkpoints
- Capture precise timestamps using hardware timers
- Format data as JSON for WebSocket transmission
- Automatic reconnection if WiFi or WebSocket drops
- Send timing data via WebSocket using simple text format: <checkpoint_id>|<elapsed_time>
```
2|3456
# 2 → checkpoint ID (STT)
# 3456 → elapsed time in milliseconds at the checkpoint
```

## Web Dashboard
- Receives real-time data via WebSocket
- Displays:
    - Checkpoint logs
    - Segment times
    - Robot progress charts
    - Frontend technologies: HTML/CSS/JS
- [GUI-Dashboard][./web.png]

## Setup & Installation
```
git clone git@github.com:MinhQuocNguyenHoang/Checkpoint-System.git
cd Checkpoint-System
# Edit config.h for WiFi SSID, server IP, checkpoint IDs
# Compile and flash to ESP32
# Run html web local 
```

## Operation Workflow
- Robot powers on → ESP32 initializes sensors and timers
- Robot passes checkpoint → IR sensor triggers interrupt
- ESP32 captures timestamp, sends simple text via WebSocket to server
- Server writes data to database, broadcasts to dashboard clients
- Dashboard updates live progress and segment times


## Future Improvements
- Add support for multiple robots simultaneously
- Implement analytics for speed, average segment time, and performance ranking
- Support long-range communication via LoRa or other protocols
- Add alert system if robot misses a checkpoint

## Authors
Nguyễn Hoàng Minh Quốc – Embedded & firmware development, system design<br>
Trần Quốc Thiện - Web
