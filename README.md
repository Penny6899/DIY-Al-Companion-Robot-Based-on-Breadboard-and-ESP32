# DIY AI Companion Robot “Xiaozhi”  

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)  
[![Build Status](https://github.com/your-org/xiaozhi/actions/workflows/ci.yml/badge.svg)](https://github.com/your-org/xiaozhi/actions)  
[![Release](https://img.shields.io/github/v/release/your-org/xiaozhi)](https://github.com/your-org/xiaozhi/releases)  
[![Issues](https://img.shields.io/github/issues/your-org/xiaozhi)](https://github.com/your-org/xiaozhi/issues)  
[![Stars](https://img.shields.io/github/stars/your-org/xiaozhi)](https://github.com/your-org/xiaozhi/stargazers)  
[![Last Commit](https://img.shields.io/github/last-commit/your-org/xiaozhi)](https://github.com/your-org/xiaozhi/commits/main)  

A breadboard-based, ESP32-powered desktop companion that listens, thinks, moves, and speaks—bridging technology and emotional support on your desk.

---

## 🚀 Key Features

- **Multi-Modal Interaction**  
  - Offline wake-word detection (ESP-SR)  
  - Real-time ASR → LLM → TTS pipeline (DeepSeek, Doubao, Qianwen)  
  - OPUS audio codec for sub-second responsiveness

- **Robust Connectivity & Control**  
  - Dual-mode Wi-Fi & ML307 Cat.1 4G fail-over  
  - WebSocket or MQTT+UDP via MCP protocol  
  - Local & cloud control of volume, lights, motors, GPIO

- **Versatile Hardware Platform**  
  - Supports ESP32-C3, ESP32-S3, ESP32-P4  
  - SSD1306 OLED & RGB LED ring  
  - 3D speaker module with voiceprint recognition  
  - Rotating camera for face and screen monitoring

- **Expressive Physical Actions**  
  1. Sit / Stand  
  2. Walk Forward (10 steps)  
  3. Turn Left / Right 90°  
  4. Head LED toggle  
  5. Ambient LED breathing  
  6. Wave “Hello”

- **Companion Persona**  
  - **Xiaozhi**: cheerful Taiwanese-accented Mandarin  
  - Pre-set female voice (TW-Cute-F01, SSML-tuned)  
  - Evaluated in small talk, comforting, jokes, and study tips

---

## 📋 Quick Start

### 1. Assemble Hardware

1. **Solder & mount** on a breadboard:  
   - ESP32 dev board, MAX98357A amp, INMP441 mic  
   - SSD1306 OLED, ML307 4G module (≥ 3 cm from mic)  
   - Servo brackets & cables for four servos  
2. **Power**: Li-ion battery → charging module → battery socket  
3. **Connect**: speaker, LEDs, camera, antenna, GPIO lines  

> See `docs/assembly.md` for detailed photos.

### 2. Flash Firmware

```bash
git clone --recursive https://github.com/your-org/xiaozhi.git
cd xiaozhi/firmware

idf.py set-target esp32s3
idf.py menuconfig        # Configure Wi-Fi / MQTT / WebSocket
idf.py flash monitor

### 3. Run & Interact

1. Plug in power → wait for LED “ready”  
2. Open companion app → issue commands:  

Sit
Forward
Turn Left
Lights On
Ambient On
Wave

📊3. Watch **Xiaozhi** move, light up, and speak back!

| Action                  | Latency  | Accuracy / Stability       | Outcome |
|-------------------------|----------|----------------------------|---------|
| Sit Down                | ~0.8 s   | ≤ 1.2° pitch variation     | PASS    |
| Forward Walk (10 steps) | 0.9 s    | 9.8 cm ± 0.4 cm, 3 mm drift| PASS    |
| Turn Left 90°           | —        | 91° ± 2°, no slip          | PASS    |
| Turn Right 90°          | —        | 90° ± 1.8°, roll < 1°      | PASS    |
| Head LED Toggle         | < 0.2 s  | brightness variance ≤ 5 %  | PASS    |
| Ambient-LED Breathing   | 3 s cycle| ΔT < 1.5 °C, no flicker    | PASS    |
| Conversational Persona  | < 1 s    | MOS > 4.0 across scenarios | PASS    |

> Full details in `docs/evaluation.md`.
