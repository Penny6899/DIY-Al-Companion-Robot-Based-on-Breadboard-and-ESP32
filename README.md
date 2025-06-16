# DIY-Al-Companion-Robot-Based-on-Breadboard-and-ESP32

# DIY AI Companion Robot “Xiaozhi”

A breadboard-based, ESP32-powered AI companion robot that listens, thinks, moves, and speaks—bringing emotional support and practical assistance right to your desk.

---

## 🚀 Features

- **Multi-Modal Interaction**  
  - Offline wake-word detection (ESP-SR)  
  - Streamed ASR → LLM → TTS (DeepSeek, Doubao, Qianwen)  
  - OPUS audio codec, sub-second response

- **Connectivity & Control**  
  - Wi-Fi + ML307 Cat.1 4G fail-over  
  - WebSocket or MQTT+UDP over MCP protocol  
  - Local & cloud device control (volume, lights, motors, GPIO)

- **Hardware Platform**  
  - ESP32-C3 / ESP32-S3 / ESP32-P4  
  - SSD1306 OLED & RGB LED ring  
  - 3D speaker module + voiceprint recognition  
  - Rotating camera for face & screen monitoring  

- **Physical Actions**  
  1. Sit / Stand  
  2. Walk Forward (10 steps)  
  3. Turn Left / Right 90°  
  4. Head LED toggle  
  5. Ambient-LED breathing effect  
  6. Wave “Hello”

- **Conversational Persona**  
  - **Xiaozhi**: cheerful Taiwanese-accented Mandarin  
  - Pre-set female voice (TW-Cute-F01, SSML-tuned)  
  - Tested in small talk, comforting, jokes, study tips

---

## 📋 Quick Start

### 1. Hardware Assembly

1. **Solder & Mount** on a breadboard:  
   - ESP32 dev board, MAX98357A amp, INMP441 mic  
   - SSD1306 OLED, ML307 4G module (keep ≥ 3 cm from mic)  
   - Servo brackets & cables for four dog-leg servos  
2. **Power**: Li-ion battery → charging module → battery socket  
3. **Connect**: speaker, LEDs, camera, antenna, GPIO lines  

> See `docs/assembly.md` for step-by-step photos.

---

### 2. Flash Firmware

```bash
# Clone and build
git clone --recursive https://github.com/your-org/xiaozhi.git
cd xiaozhi/firmware

# Configure & flash to your ESP32
idf.py set-target esp32s3
idf.py menuconfig        # set Wi-Fi / MQTT / WebSocket options
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

3. Watch **Xiaozhi** move, light up, and speak back!

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
