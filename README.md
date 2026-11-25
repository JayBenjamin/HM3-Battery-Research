# HM3 Battery Research (`HM3-Battery-Research`)

> **CRITICAL SAFETY & REGULATORY NOTICE — BENCH RESEARCH ONLY**
>
> This repository documents an **open-source hardware evaluation platform, reverse-engineering log, and hemodynamic Hardware-in-the-Loop (HIL) test bench**. None of the hardware, firmware, schematics, or CAD files here are FDA-cleared, PMA-approved, or IEC 60601 / IEC 62133 certified. **NEVER** connect experimental, DIY, modified, or uncertified battery packs, cables, or electronics to life-sustaining medical equipment. All testing is performed exclusively on expired, decommissioned, non-clinical surplus bench hardware and programmable electronic loads. See [`SAFETY.md`](SAFETY.md) before proceeding.

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
![Status: Phase 2](https://img.shields.io/badge/Status-Phase%202%20%E2%80%94%20Bench%20Probing-orange)

---

## The Mission: Ending the "Square One" Trap

For over a decade, external power hardware for durable Left Ventricular Assist Devices (LVADs) such as the HeartMate 3 has remained locked into mid-2000s lithium-ion cell topologies (dual 8-cell `4S2P 18650` packs). Carrying two legacy packs and clips means hauling roughly **3.5 to 3.7 lbs (~1,600–1,680 g)** every day, while closed-door academic studies and corporate R&D roadmaps continually promise breakthroughs "five years away" without publishing actionable engineering data.

This project exists to change that dynamic through three core commitments:

1. **Building the "Missing Manual" in Public:** Every pinout mapped, logic-analyzer capture recorded, and teardown documented permanently removes the "square one" barrier so engineers, students, and researchers never have to start from scratch.
2. **Proving What Is Possible Today:** Demonstrating on a live, open-source bench prototype how modern `21700` cells (~260+ Wh/kg) achieve **~55%–78% weight reductions**, open cell-level health telemetry, and universal **USB-C Power Delivery** charging.
3. **Catalyzing Industry Progress:** Establishing a transparent, reproducible engineering benchmark to shift expectations and encourage OEMs, competitors, and research labs to prioritize lighter, safer, modern external power systems.

---

## Target Weight & Runtime Comparison (Speculative Bench Baseline)

*Baseline: `1x Samsung INR21700-50G` = ~69.5 g, 21.25 × 70.8 mm, 5,000 mAh / ~18 Wh (~72–74 Wh per `4S1P` bank).*

| Configuration | Cell Count & Topology | Raw Cell Weight | Est. Finished Weight | Approx. Cell Core Size | Est. Runtime (vs. 18 hr Dual OEM) | Notes / Use Case |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **OEM Dual Setup (Baseline)** | `16x 18650` (`2× 4S2P` + 2 clips) | ~735 g (1.62 lbs) | **~1,600–1,680 g (~3.5–3.7 lbs)** | Two VHS-sized bricks + clips | ~14–18 hrs (~142–150 Wh) | Heavy, bulky; exposed 7-pad clip wear |
| **Single `4S1P` 21700** | `4x 21700` (`50G`) | ~278 g (0.61 lbs) | **~350–380 g (~0.78–0.83 lbs)** | ~84 × 70 × 21 mm (deck of cards) | **~7.5–8.5 hrs** (~72–74 Wh) | **~78% lighter** than dual OEM; ultra-light bench target |
| **Two `4S1P` 21700 Packs** | `8x 21700` (2 independent packs) | ~556 g (1.23 lbs) | **~700 g (~1.55 lbs) total** | Two slim deck-of-cards units | **~15–17.5 hrs** (~144–148 Wh) | **~56% lighter** (~2 lbs saved); true dual-pack isolation |
| **Single 8-Cell `2×4S1P` Pack** | `8x 21700` (dual bank, 1 shell) | ~556 g (1.23 lbs) | **~660–680 g (~1.45–1.50 lbs)** | ~145 × 85 × 22 mm (paperback) | **~15–17.5 hrs** (~144–148 Wh) | Lighter than *one* clipped OEM pack while doing the job of two |
| **Ultralight `4S1P` 18650 Sprint** | `4x 18650` (modern `3,500 mAh`) | ~180 g (0.40 lbs) | **~250 g (~0.55 lbs) per pack** | ~72 × 65 × 18 mm | ~5–6 hrs per pack (~50 Wh) | Optional future pocket-sized variant |

---

## Repository Structure

```text
HM3-Battery-Research/
├── README.md                          # Project overview, mission, targets & roadmap
├── LICENSE                            # MIT License
├── SAFETY.md                          # Non-clinical boundaries, Li-Ion & HIL safety rules
├── docs/
│   ├── OEM_FAILURE_ANALYSIS.md        # HeartMate I→II→3→FILVAS timeline, FDA MAUDE & recalls FMEA
│   ├── SYSTEM_ARCHITECTURE.md         # 4S1P 21700 power, IP2368 65W PD, 3-layer protection & waterproofing
│   └── MCU_AND_CELL_SELECTION.md      # Samsung 50G specs & ESP32-S3 / M5Stack board evaluation
├── reverse-engineering/
│   ├── thoratec-102515/               # 4-donor inventory, verified 7-pad pinout, photos & teardown logs
│   ├── battery-clip-2865/             # 5-pin circular connector findings & continuity sweep plan
│   ├── mobile-power-unit-mpu/         # 10-pin connector findings, AC watt baselines & teardown plan
│   └── captures/                      # PulseView / Saleae .sr SMBus & UART captures (Milestone 3)
├── hardware/                          # Breadboard diagrams, KiCad PCB, Ideal-Diode OR-ing & BOM.csv
├── enclosure/                         # Splash-proof daily shell, IP68 shower housing & thermal liners
├── firmware/                          # BMS telemetry, SMBus/UART sniffer, power management & IMU UI
└── hil-simulator/                     # Python SCPI hemodynamic load controller, web UI & test logs
```

---

## Six-Milestone Roadmap

| Milestone | Scope | Status |
| :--- | :--- | :--- |
| **1. Research, FMEA & Sourcing** | 21700 evaluation, `20x Samsung INR21700-50G` & `4x Thoratec 102515` donors acquired, FDA MAUDE/recall FMEA, `4,900 RPM` AC watt baselines. | **Completed** |
| **2. Non-Invasive Probing & Mapping** | `0.000V` dead-donor lockout, live `Rev. L` 7-pad pinout, `2865` clip (5-pin) vs. `MPU` (10-pin) connectors. *Next:* clip continuity sweep, `0.01V` meter & USB logic analyzer. | **In Progress** |
| **3. Destructive Teardowns & Bus Decoding** | Open `ML031100` (`Rev. F`) & surplus `MPU`, trace internal PCBs/ICs, capture live SMBus (`0x0B`) & UART frames. | **Next Up** |
| **4. MCU & `4S1P` Breadboard Prototype** | Finalize `ESP32-S3`/`M5Stack` board; wire swappable `4S1P` bank with hardware BMS IC, thermal fuse, `IP2368` `65W` PD & Ideal-Diode OR-ing. | **Planned** |
| **5. AI Hemodynamic HIL Test Bench** | Assemble SCPI electronic load rig inside fireproof containment (`60°C` hardware cutoff) and publish open CSV/JSON validation logs. | **Planned** |
| **6. Mechanical CAD & Variants** | Finalize splash-proof daily `PA-CF` shell & external `IP68` shower over-housing across 4-cell and 8-cell variants. | **Future** |

---

## Companion Research & Voluntary R&D Support

* **Prior Emergency & Off-Grid Power Research:** [HeartMate 3 Power Survival Guide: Solutions for LVAD Emergencies & Off-Grid Living](https://jbbenjamin.com/heartmate-3-power-survival-guide-solutions-for-lvad-emergencies-off-grid-living/) (empirical `4,900 RPM` MPU & UBC watt-meter baselines and tiered outage backup guide).
* **No Commercial Hardware Sales:** This project does not sell assembled battery packs, medical accessories, or lithium-ion cells. All designs use standard general-purpose terminations (**XT60**, **4-pin JST-GH / Grove I²C** + **UART**, **USB-C PD**).
* **Support Open-Source R&D:** Bench instrumentation, surplus teardowns, and destructive safety testing are self-funded and supported solely by voluntary community contributions via the [OpenHeart Research Fund](https://square.link/u/YXz3dqBN).

## Runtime Reconciliation (Option A)

- **AC Wall Baseline:** `6.47 W` average (`5.48 W - 7.46 W` typical; `10.15 W` initial connection spike) at `4,900 RPM` on AC watt meter.
- **DC Load Basis:** `8.0 W` DC mixed-activity planning draw (`~5.5 W` DC resting equivalent derived from `6.47 W` AC with `0.85` MPU supply efficiency and controller overhead accounted for).
- **Formula:** `Runtime_h = (Wh * 0.90) / 8.0 W` -> `~8.1-8.4 hrs` for a single `72-74 Wh` `4S1P Samsung INR21700-50G` pack and `~16.2-16.8 hrs` for dual `4S1P` packs.

## Populated vs. Planned Folders

- **Active content so far:** `docs/`, `reverse-engineering/`, and `images/`.
- **Planned stubs:** `hardware/`, `firmware/`, `enclosure/`, `hil-simulator/`, `scans/`, and `research/`.
