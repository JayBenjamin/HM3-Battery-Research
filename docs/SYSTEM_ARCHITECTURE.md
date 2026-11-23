# Target 4S1P 21700 Architecture, Protection & Enclosure Strategy

> **Bench Research Only:** All specifications below describe a non-clinical open-source hardware evaluation architecture using standard general-purpose connectors.

## 1. Power Topology & Bidirectional USB-C PD (`IP2368`)

* **Cell Topology:** `4S1P` using `Samsung INR21700-50G` (`3.63V` nominal, `4.20V` full charge, `2.50V` cutoff, `5,000 mAh` typical).
* **Pack Energy:** `14.52V–14.8V` nominal (`16.8V` max), delivering **~72–74 Wh** using **4 cells instead of 8**—matching or exceeding the legacy `71 Wh` `Thoratec 102515` pack while halving cell count, spot-weld points, and parallel-bank failure modes.
* **Bidirectional USB-C Power Delivery (`IP2368` Buck-Boost):**
  * Supports universal charging from standard USB-C PD wall adapters and 12V automotive outlets, eliminating proprietary open-bay desktop docks.
  * **`65W` Charge Cap (`~3.8A` at `16.8V`):** Intentionally capped at `65W` rather than `100W` (`~6A`) so charge current stays safely inside the `Samsung INR21700-50G` `4.85A` (`1C`) datasheet ceiling—delivering a full 0–100% charge in ~1 hr 25 min (20–80% in ~45 min) while preserving 500+ cycle longevity.
* **Auxiliary Phone Charging with SoC Reserve Cutoff:**
  * Bidirectional USB-C PD output allows emergency smartphone charging governed by an MCU-enforced **State-of-Charge (SoC) reserve cutoff** (default **`50%` SoC floor**) so auxiliary phone charging can never drain primary reserves.
* **Strict Thermal Charge Gating (`0°C–45°C`):**
  * Multi-point `10kΩ` NTC thermistors placed against cell cores and power connectors enforce hard `0°C` low-temperature and `45°C` high-temperature charging cutoffs (`60°C` discharge over-temperature limit).

---

## 2. Three-Layer Hardware Safety & Dual-Rail Isolation

To ensure safety never relies solely on microcontroller firmware:

1. **Dedicated Hardware BMS Protection IC:** Independent analog/hardware comparator stage enforcing per-cell overvoltage (`>4.25V`), undervoltage (`<2.50V`), overcurrent, and short-circuit MOSFET disconnect.
2. **Non-Resettable Secondary Thermal / Overcurrent Fuse:** Physical three-terminal chemical/thermal fuse in series with the main pack rail as a last-resort failsafe if primary FETs weld closed.
3. **Ideal-Diode OR-ing Isolation (`LM5050` / `LTC4412` / `LM74700-Q1`):** Low-loss active MOSFET OR-ing controllers act as one-way electrical valves across dual packs or dual output rails—enabling zero-drop, zero-backfeed power sharing and hot-swapping without direct parallel (`2P`) cell wiring.

---

## 3. General-Purpose Interfaces Only

* **Power Output:** Standard **XT60** high-current connector.
* **Charging / Aux Output:** Standard **USB-C PD** receptacle.
* **Digital Telemetry Headers:** Standard **4-pin JST-GH / Grove** I²C header (`V+`, `GND`, `SDA`, `SCL`) paired with a dedicated **UART header** (`TX`, `RX`, `GND`), plus Wi-Fi/BLE WebSocket & CSV telemetry streaming.

---

## 4. Mechanical Modularity & Two-Tier Water Protection

* **Breadboard-First Modularity:** Final housing geometry is deferred until the core `4S1P` electrical, BMS, and telemetry stack is validated on the breadboard. Once validated, the same electronics drop into 4-cell, dual 4-cell, or 8-cell form factors.
* **Self-Enclosed Electronics with Swappable Cells:** All BMS, charging, and telemetry electronics live inside one self-enclosed housing while keeping the `21700` cells **removable and swappable** (no permanent epoxy potting over cells).
* **Passive Thermal Isolation:** 3D-printed **Carbon Fiber Reinforced Nylon (`PA-CF`)** or `ASA` shell with internal cell isolation channels and passive thermal liners.
* **Two-Tier Water Protection:**
  1. **Tier 1 — Splash-Proof Daily Enclosure:** Gasketed `PA-CF` / `ASA` shell with recessed `XT60` / `USB-C` ports engineered to resist sweat, humidity, and accidental splashes while preserving cell access.
  2. **Tier 2 — External `IP68` ("Scuba Gear") Shower Over-Housing:** Rigid, gasket-sealed waterproof outer shell with sealed cable pass-throughs that slips over the daily pack during high-moisture exposure.
