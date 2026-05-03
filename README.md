# Star Trek Tricorder Rev2 — PCB & Schematics

> KiCad schematic and PCB layout files for the Star Trek Tricorder Rev2. The hardware is distributed across three boards — Tricorder Main, Tricorder Sensor, and Tricorder LED Array 2 — interconnected via a 20-pin FFC cable.

![Status](https://img.shields.io/badge/status-work%20in%20progress-orange)
![Tool](https://img.shields.io/badge/designed%20in-KiCad-blue)
![Author](https://img.shields.io/badge/author-Vishal%20Soni-teal)

---

## Table of Contents

- [Board Overview](#board-overview)
- [Tricorder Main](#tricorder-main)
- [Tricorder Sensor](#tricorder-sensor)
- [Tricorder LED Array 2](#tricorder-led-array-2)
- [Interconnect](#interconnect--ffc-cable)
- [Repository Structure](#repository-structure)
- [Tools Used](#tools-used)
- [Related Repositories](#related-repositories)
- [Credits](#credits)

---

## Board Overview

The hardware is split across three dedicated PCBs to keep the design modular and assembly manageable within the compact Tricorder enclosure.

| Board | Role | Files Available |
|---|---|---|
| Tricorder Main | Central controller — ESP32S3, display, audio, touch input | Schematic + Layout |
| Tricorder Sensor | Environmental sensing, power monitoring, LED array 1 | Layout only |
| Tricorder LED Array 2 | Secondary WS2812B LED array | Schematic + Layout |

All boards are KiCad projects and communicate over a shared **I²C bus** via a **20-pin 1mm pitch FFC cable**.

---

## Tricorder Main

The Main PCB is the central control unit built around the **Seeed Studio XIAO ESP32S3**. It sits directly below the TFT display and coordinates all subsystems.

**Files:** Schematic + Layout

### Interfaces

| Interface | Protocol | Connected To |
|---|---|---|
| TFT Display (ST7735) | SPI (MOSI, SCK, CS, DC, RST) | ST7735 1.8" TFT |
| Audio Module (JQ6500) | UART (TX/RX) | JQ6500 |
| GPIO Expander (MCP23008) | I²C (SDA/SCL) | TTP223 touch inputs ×6 |
| LED Array — Primary | Single-wire (WS2812B protocol) | WS2812B LEDs |
| FFC Connector | 20-pin, 1mm pitch | Tricorder Sensor board |

### Key ICs

| IC / Module | Function |
|---|---|
| Seeed Studio XIAO ESP32S3 | Main microcontroller |
| MCP23008 | I²C GPIO expander for touch input routing |
| JQ6500 | UART audio playback module |
| TTP223 ×6 | Capacitive touch sensors |
| WS2812B (2020) | Addressable RGB LEDs — primary array |

---

## Tricorder Sensor

The Sensor Panel contains all environmental sensing and power monitoring components, along with LED Array 1. It connects to the Main PCB entirely over the FFC cable.

**Files:** Layout only

### Interfaces

| Interface | Protocol | Connected To |
|---|---|---|
| Environmental Sensor (BME280) | I²C | Shared I²C bus |
| Power Monitor (INA219) | I²C | Shared I²C bus |
| LED Array 1 | Single-wire (WS2812B protocol) | WS2812B LEDs |
| FFC Connector | 20-pin, 1mm pitch | Tricorder Main board |

### Key ICs

| IC / Module | Function |
|---|---|
| DFRobot BME280 | Temperature, pressure, and altitude sensing |
| INA219 | Voltage, current, and power monitoring |
| WS2812B (2020) | Addressable RGB LEDs — array 1 |

---

## Tricorder LED Array 2

A dedicated board for the secondary WS2812B LED array.

**Files:** Schematic + Layout

### Specifications

| Parameter | Value |
|---|---|
| PCB Material | FR4 |
| Board Thickness | 0.6 mm |

### Key IC

| IC / Module | Function |
|---|---|
| WS2812B (2020) | Addressable RGB LEDs — array 2 |

---

## Interconnect — FFC Cable

All boards communicate over a **20-pin, 1mm pitch FFC cable**, which carries:

| Signal Group | Lines |
|---|---|
| Power | VCC, GND |
| I²C Bus | SDA, SCL |
| LED Control | WS2812B data line |
| Miscellaneous | Additional control and status signals |

Using FFC keeps internal wiring clean, reduces assembly complexity, and allows each board to be removed or replaced independently.

---

## Repository Structure

```
tricorder-rev2-circuits/
│
├── tricorder-main/
│   ├── tricorder-main.kicad_pro
│   ├── tricorder-main.kicad_sch
│   ├── tricorder-main.kicad_pcb
│   └── gerbers/
│
├── tricorder-sensor/
│   ├── tricorder-sensor.kicad_pro
│   ├── tricorder-sensor.kicad_pcb
│   └── gerbers/
│
├── tricorder-led-array-2/
│   ├── tricorder-led-array-2.kicad_pro
│   ├── tricorder-led-array-2.kicad_sch
│   ├── tricorder-led-array-2.kicad_pcb
│   └── gerbers/
│
└── docs/
    └── block-diagram.png
```

---

## Tools Used

| Tool | Purpose |
|---|---|
| [KiCad](https://www.kicad.org/) | Schematic capture and PCB layout |

---

## Related Repositories

| Repository | Contents |
|---|---|
| [Tricorder Rev2 — Firmware](https://github.com/vishalqsoni/Tricoder-Rev2/tree/main) | Arduino firmware, UI, sensors, animations |
| [Tricorder Rev2 — 3D Models](#) | Enclosure and mechanical files |

---

## Credits

- **PCB Design & Hardware** — [Vishal Soni](https://github.com/vishalqsoni)
- **3D Printing** — [JustWay](https://justway3d.com)
- **Firmware**- [Vishal Soni](https://github.com/vishalqsoni)

---

## License

MIT License — see [LICENSE](LICENSE) for details.
