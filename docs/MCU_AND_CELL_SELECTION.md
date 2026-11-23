# Cell Chemistry & Microcontroller Evaluation

## 1. Modern Medical-Grade 21700 Context
Contemporary FDA-cleared portable medical equipment (AEDs, transport ventilators, infusion pumps, powered surgical tools) increasingly standardizes on **UL 1642 / IEC 62133-2 certified `21700` Lithium-Ion cells** paired with impedance-tracking smart gas-gauge ICs (`TI bq40zxx` family), multi-point NTC thermistors, and dual-stage hardware protection.

## 2. 21700 Cell Baseline (`Samsung INR21700-50G` — On Hand)

| Parameter | `Samsung INR21700-50G` (Baseline) | Optional High-Rate Path (`Molicel P45B` / `P50B`) |
| :--- | :--- | :--- |
| **Nominal Voltage** | `3.63V` (`4.20V` max / `2.50V` cutoff) | `3.60V` |
| **Typical Capacity** | `5,000 mAh` (`4,900 mAh` std / `4,750 mAh` at 1C) | `4,500–5,000 mAh` |
| **Pack Energy (`4S1P`)** | `~72–74 Wh` | `~65–72 Wh` |
| **Continuous Discharge** | `9.7A–9.8A` (`2C`); `14.7A` pulse | `45A+` |
| **Charge Envelope** | `2.45A` (`0.5C`) std / `4.85A` (`1C`) max | Up to `13.5A–25A` |
| **USB-C PD Target** | **Capped at `65W` (`~3.8A` at `16.8V`)** | Supports full `100W` (`~6A`) fast charging |
| **Bench Status** | **20x cells on hand** (`SAMSUNG SDI 2M32`, `3.518V` resting) | Future optional variant |

---

## 3. Microcontroller & Telemetry Platform Evaluation (Open)

Final carrier board selection remains open during the breadboard phase while evaluating `ESP32-S3` and `M5Stack`-class modules:

| Candidate Platform | Strengths | Best Phase Fit |
| :--- | :--- | :--- |
| **Compact `ESP32-S3` Modules** (`Seeed XIAO ESP32-S3`, `ESP32-S3 N16R8`, `Waveshare ESP32` LCD) | Ultra-compact footprint, native USB, Wi-Fi/BLE, ample GPIO/I²C/UART buses for custom carrier PCB integration. | Custom carrier PCB (Milestone 4+) |
| **`M5Stack` Integrated Units** (`AtomS3R`, `M5StickC PLUS2`, `CoreS3`) | Pre-integrated IPS screens, physical buttons, buzzers, Grove connectors, and 6-axis IMUs (`BMI270` / `MPU6886`). | Rapid breadboard prototyping & bench dashboards |

### Core Telemetry & Sensor Requirements
* **Cell & Pack Health:** Per-cell voltage monitoring, high-side shunt current sensing, coulomb counting, internal resistance tracking (State-of-Health), and multi-point `10kΩ` NTC temperatures.
* **Motion & Activity Context (`QMI8658` / `BMI270` 6-Axis IMU):** Step counting, activity correlation, and fall/impact event detection.
* **Open Bus Interfaces:** `4-pin JST-GH / Grove` I²C (`V+`, `GND`, `SDA`, `SCL`), dedicated `UART` (`TX`, `RX`, `GND`), and Wi-Fi/BLE WebSocket + CSV logging.
