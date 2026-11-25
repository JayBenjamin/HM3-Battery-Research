# System Architecture & Telemetry Data Flow

`4S1P Pack (XT60)` -> `Hardware BMS + NTC + Ideal-Diode OR-ing` -> `ESP32-S3 / Telemetry Bus (I2C / UART)` -> `WebSocket` -> `Web Dashboard` -> `Logs`

## Planned Folder Hierarchy (Reference)

Future directories and submodules are mapped here so active navigation stays focused on collected bench data and current work:

```text
HM3-Battery-Research/
|-- hardware/
|   |-- breadboard-prototype/
|   |-- carrier-pcb/
|   `-- ideal-diode-combiner/
|-- firmware/
|   |-- bms-telemetry/
|   |-- power-management/
|   |-- smbus-uart-sniffer/
|   `-- ui-and-imu/
|-- enclosure/
|   |-- daily-splash-shell/
|   |-- ip68-shower-housing/
|   |-- thermal-liners/
|   |-- STL/
|   `-- STEP/
|-- hil-simulator/
|   |-- scpi-load-controller/
|   |-- test-logs/
|   `-- web-dashboard/
|-- scans/
|   |-- raw/
|   |-- cleaned/
|   `-- reference/
`-- research/
```
