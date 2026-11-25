# Firmware Architecture (`ESP32-S3` / `M5Stack`)

**Status:** Planned

* `bms-telemetry/` — Per-cell voltages, high-side shunt current, coulomb counting, internal resistance (SOH), and `0°C–45°C` NTC thermal gating.
* `smbus-uart-sniffer/` — Passive decoder tools for OEM SMBus (`0x0B`) and white-cable UART frames.
* `power-management/` — `IP2368` `65W` charge cap control and `50%` SoC reserve cutoff for auxiliary USB-C phone charging.
* `ui-and-imu/` — Onboard LCD display, BLE/Wi-Fi WebSocket streaming, and `QMI8658`/`BMI270` 6-axis IMU activity & impact alerts.

## How to Build / Run This

Not yet available.
