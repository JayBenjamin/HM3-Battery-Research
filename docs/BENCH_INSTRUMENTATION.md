# Lab Bench Instrumentation & Equipment Roadmap

> **BENCH RESEARCH ONLY:** All instrumentation below is used exclusively for non-clinical reverse engineering on expired, decommissioned surplus hardware and programmable electronic load validation. See [`SAFETY.md`](../SAFETY.md) for Li-Ion teardown and HIL fire-containment protocols.

---

## 1. Current Bench Gear (On Hand)

| Equipment | Model / Spec | Current Role & Limitations |
| :--- | :--- | :--- |
| **Multimeter** | `Commercial Electric BMM-8132R` | Used for initial `0.000V` dead-donor lockout checks and live `Rev. L` 7-pad DC (`V⎓`) sweeps. **Limitations:** `1V` whole-volt DC resolution (cannot audit individual `4S2P` cell banks accurately) and `2kΩ` resistance ceiling (standard `10kΩ` NTC thermistors read over-range `OL`). |

---

## 2. Planned Bench Instrumentation Roadmap (Researched — Not Yet Ordered)

| Tool Category | Candidate Models | Purpose on Bench | Target Milestone |
| :--- | :--- | :--- | :--- |
| **Multimeter (Upgrade)** | Any `0.01V` (`20V DC`) / `>20MΩ` meter | Replaces `BMM-8132R` for accurate `4S2P` internal cell-bank audits (`B-`→`B1`→`B2`→`B3`→`B+`) and `10kΩ` NTC thermistor / pull-down measurements. | Milestone 2 → 3 |
| **USB Logic Analyzer** | **Budget:** `Cypress FX2LP` 8-Ch 24MHz (`~$15`, `PulseView`)<br>**Mid:** `DSLogic Plus` (`~$100`)<br>**Pro:** `Saleae Logic 8` (`~$400+`) | Passively sniffing `100 kHz` SMBus / I²C (`0x0B` Smart Battery Data registers) on live battery pads (`Pads 4 & 5`) and UART / RS-485 telemetry on the white MPU / System Controller cable. | Milestone 3 |
| **Active Bus Emulators** | `FTDI FT232RL` / `CP2102` (`~$5`) + `RP2040` / `ESP32` (`~$4–$10`) | Active "talker" to emulate an SMBus `0x0B` battery or UART monitor while the logic analyzer passively records bus traffic. | Milestone 3 → 4 |
| **Programmable DC Bench PSU** | **Budget:** `Wanptek 30V 10A` (`~$59`) or `Korad KD3005P` (USB/CSV)<br>**Mid:** `OWON SPE3051` / `Agilent E3646A` (used)<br>**Lab:** `Rigol DP832` / `Siglent SPD3303X-E` | Current-limited waking/charging (`16.8V`, `0.2A`), BMS bring-up, automated charge cycling, and CSV data logging. | Milestone 4 |
| **Programmable DC Electronic Load** | `Korad KEL103`, `Rigol DL3021`, or `Siglent SDL1020X` | SCPI-controlled dynamic load profiles (resting `4,900 RPM` baseline, 2-second Artificial Pulse spikes, PI drops, exertion, and fault injection) for the AI Hemodynamic HIL test bench. | Milestone 5 |

---

## 3. Mandatory Bench & HIL Safety Hardware

* **Teardown Prep (Milestone 3 — Legacy `4ICR19/65-2` Packs):** Controlled vise/clamp, rotary seam scorer (kept strictly `< 1.5 mm` depth), non-conductive plastic/ceramic spudgers, safety glasses, non-flammable work surface, and dry sand / Li-Ion fire containment.
* **HIL Test Chamber (Milestone 5):** Vented steel / fireproof test enclosure with a clear polycarbonate viewing window for the IP/NDI camera, paired with an independent **`60°C` hardware thermal cutoff relay** that physically disconnects the load regardless of software or MCU state.