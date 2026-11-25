# Safety, Regulatory Boundaries & Lab Bench Protocols

## 1. Non-Clinical Research Scope
* **Not a Medical Device:** Nothing in this repository is FDA-cleared, PMA-approved, or certified under IEC 60601 or IEC 62133. Nothing documented here is intended for clinical, diagnostic, therapeutic, or patient life-support use.
* **Strict Off-Patient Rule:** **NEVER** connect experimental, DIY, modified, or uncertified battery packs, cables, or electronics to life-sustaining medical equipment. All bench work is restricted exclusively to expired, decommissioned surplus hardware and programmable electronic loads.
* **General-Purpose Interfaces Only:** All prototype designs standardize on non-proprietary hobbyist/industrial connectors (**XT60**, **4-pin JST-GH / Grove I²C**, **UART**, and **USB-C PD**).

## 2. Lithium-Ion & Legacy ICR Teardown Safety
* **Legacy `4ICR19/65-2` Chemistry Hazard:** Surplus `Thoratec 102515` packs contain `8x 18650 ICR` (Lithium Cobalt Oxide) cells in a `4S2P` array. Legacy ICR cells have a lower thermal runaway threshold than modern INR cells.
  * Confirm `0.000V` external lockout before handling, and **still treat internal cells as potentially energized** until every internal series tap (`B-` through `B+`) is measured.
  * When separating ultrasonic housing seams, keep rotary cutting depth **strictly under `1.5 mm`** and finish separation with controlled vise pressure and non-conductive plastic/ceramic spudgers.
  * Perform all teardowns on a non-flammable surface with safety glasses, insulated tools, and a bucket of dry sand / Class D / Li-Ion fire containment nearby.
* **Samsung `INR21700-50G` Electrical & Thermal Limits:**
  * **Charging Cap:** Keep continuous charge current **≤ `4.85A` (`1C`)** — enforced via our **`65W` USB-C PD cap (`~3.8A` at `16.8V`)**. Do not apply `100W` (`~6A`) charging to a single `4S1P 50G` bank.
  * **Thermal Charge Gating:** Hard hardware/firmware cutoff below **`0°C`** and above **`45°C`** during charging (`60°C` max discharge cutoff).
  * **Three-Layer Hardware Safety:** Never rely solely on MCU firmware for protection. Every prototype requires (1) an independent hardware BMS protection IC, (2) a non-resettable three-terminal thermal/overcurrent fuse, and (3) Ideal-Diode OR-ing (`LM5050` / `LTC4412`) for dual-rail isolation.

## 3. Public HIL Test Bench Containment Guardrails
When operating the automated Hardware-in-the-Loop (HIL) simulator:
1. **Hard-Coded SCPI Load Clamps:** Remote web inputs are clamped in the Python controller (e.g., `12W–15W` max continuous draw, queued 60-second slots). Raw amperage or dead-short commands are never exposed.
2. **Fireproof Containment:** Test packs run inside a vented steel / fireproof enclosure with a polycarbonate viewing window for the IP/NDI camera.
3. **Independent Hardware Cutoff Relay:** A standalone thermal relay physically disconnects the load above **`60°C`**, independent of software or MCU state.

## Milestone 5 Public Remote-Controlled Rig

- **Unattended Operation Policy:** No unattended overnight remote runs; require bounded active sessions inside fireproof containment.
- **Controller Watchdog:** Drop load to safe off-state if the web controller stops responding or misses heartbeats.
- **Smoke & Heat Cutoff:** Dedicated smoke/heat detection tied to a hardware cutoff relay in addition to the `60 C` hardware thermal cutoff relay.
