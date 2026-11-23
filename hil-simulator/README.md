# AI Hemodynamic Hardware-in-the-Loop (HIL) Test Bench

**Status:** Planned (Milestone 5)

An automated, live-streamed bench rig that validates the open-source `4S1P 21700` battery under realistic pump load profiles without touching clinical hardware.

* **Calibrated Baseline (`4,900 RPM`):** Anchored to empirical AC watt-meter baselines (`6.47 W` steady-state average, `5.48–7.46 W` typical envelope, `10.15 W` initial connection spike) plus asynchronous 2-second Artificial Pulse spikes.
* **Mandatory Public-Rig Safety Guardrails:**
  1. Hard-coded Python SCPI load clamps (`12W–15W` max continuous draw, queued 60-second user slots).
  2. Vented steel / fireproof test chamber with polycarbonate viewing window for the IP/NDI camera.
  3. Independent **`60°C` hardware thermal cutoff relay**.
