# AI Hemodynamic Hardware-in-the-Loop (HIL) Test Bench

**Status:** Planned

An automated, live-streamed bench rig that validates the open-source `4S1P 21700` battery under realistic pump load profiles without touching clinical hardware.

* **Calibrated Baseline (`4,900 RPM`):** Anchored to empirical AC watt-meter baselines (`6.47 W` steady-state average, `5.48–7.46 W` typical envelope, `10.15 W` initial connection spike) plus asynchronous 2-second Artificial Pulse spikes.
* **Mandatory Public-Rig Safety Guardrails:**
  1. Hard-coded Python SCPI load clamps (`12W–15W` max continuous draw, queued 60-second user slots).
  2. Vented steel / fireproof test chamber with polycarbonate viewing window for the IP/NDI camera.
  3. Independent **`60°C` hardware thermal cutoff relay**.

## Hemodynamic-to-Electrical HIL Load Profiles (Bench)

* **Baseline & Rail Modeling:** Model continuous draw and controller overhead on the dual `XT60` DC bus feeding the UART-scripted programmable DC electronic load, with `I2C` shunt/fuel-gauge logging and `USB-C PD` charging capped at `65W` (`~3.8A` for `4S1P Samsung INR21700-50G` cells, `0°C–45°C` NTC charge gate, `60°C` hardware cutoff).
* **0.5 Hz Pulse Modulation:** Emulate a `2.00 s` period (`0.15 s` trough, `0.20 s` peak, `1.65 s` baseline dwell) while polling `I2C` current/voltage sensors fast enough (`>= 20–30 Hz`) to avoid aliasing edges.
* **PI Event & Ramp-Back Transients:** Script step-downs to `Low Speed Limit` followed by controlled recovery ramps (`100 RPM/s` reference rate on HM3) to test estimator and rail tracking during non-stationary loads.
* **Failover & Hot-Swap Vectors:** Test single-pack `XT60` hot-swap disconnects across Ideal-Diode OR-ing (`LM5050` / `LTC4412` / `LM74700-Q1`) and dual-rail disconnects onto a `3S` (`11.1V` nominal) backup rail (`>= 15 min` full-load window followed by `Power-Saver` step-down).

## How to Build / Run This

Not yet available.

## Milestone 5 Public Remote-Controlled Rig Guardrails

- **Unattended Operation Policy:** No unattended overnight remote runs; require bounded active sessions inside fireproof containment.
- **Controller Watchdog:** Drop load to safe off-state if the web controller stops responding or misses heartbeats.
- **Smoke & Heat Cutoff:** Dedicated smoke/heat detection tied to a hardware cutoff relay in addition to the `60 C` hardware thermal cutoff relay.
