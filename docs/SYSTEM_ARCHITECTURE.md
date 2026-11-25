# System Architecture & Telemetry Data Flow

`4S1P Pack (XT60)` -> `Hardware BMS + NTC + Ideal-Diode OR-ing` -> `ESP32-S3 / Telemetry Bus (I2C / UART)` -> `WebSocket` -> `Web Dashboard` -> `Logs`

- **Locked Baseline:** `4S1P Samsung INR21700-50G` (`20x` on hand at `3.518V` resting), `IP2368` USB-C PD capped at `65W` (`~3.8A` at `16.8V` for `1C` / `4.85A` safety), `0\u00b0C\u201345\u00b0C` NTC charge gating, `60\u00b0C` hardware cutoff, `50%` SoC auxiliary phone-charging floor, three-layer hardware safety (hardware BMS IC + 3-terminal thermal fuse + `LM5050` / `LTC4412` / `LM74700-Q1` Ideal-Diode OR-ing), splash-proof daily shell + separate `IP68` shower over-housing, and general-purpose connectors (`XT60`, `USB-C PD`, `4-pin JST-GH / Grove I2C`, `UART`).

## Planned Folder Hierarchy (Reference)

Future directories and submodules are parked here so active repository navigation stays focused on collected bench data and current work:

```text
HM3-Battery-Research/
\u251c\u2500\u2500 hardware/
\u2502   \u251c\u2500\u2500 breadboard-prototype/
\u2502   \u251c\u2500\u2500 carrier-pcb/
\u2502   \u2514\u2500\u2500 ideal-diode-combiner/
\u251c\u2500\u2500 firmware/
\u2502   \u251c\u2500\u2500 bms-telemetry/
\u2502   \u251c\u2500\u2500 power-management/
\u2502   \u251c\u2500\u2500 smbus-uart-sniffer/
\u2502   \u2514\u2500\u2500 ui-and-imu/
\u251c\u2500\u2500 enclosure/
\u2502   \u251c\u2500\u2500 daily-splash-shell/
\u2502   \u251c\u2500\u2500 ip68-shower-housing/
\u2502   \u251c\u2500\u2500 thermal-liners/
\u2502   \u251c\u2500\u2500 STL/
\u2502   \u2514\u2500\u2500 STEP/
\u251c\u2500\u2500 hil-simulator/
\u2502   \u251c\u2500\u2500 scpi-load-controller/
\u2502   \u251c\u2500\u2500 test-logs/
\u2502   \u2514\u2500\u2500 web-dashboard/
\u251c\u2500\u2500 scans/
\u2502   \u251c\u2500\u2500 raw/
\u2502   \u251c\u2500\u2500 cleaned/
\u2502   \u2514\u2500\u2500 reference/
\u2514\u2500\u2500 research/
```
