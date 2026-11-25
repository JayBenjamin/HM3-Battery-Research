# Contributing & Bench Workflow

## Support Open-Source R&D
Bench instrumentation, surplus teardowns, 3D scan/CAD work, and destructive safety testing are self-funded and supported solely by voluntary community contributions via the **[Square R&D Fund](https://square.link/u/YXz3dqB6)** (no commercial hardware sales; personal receipts and Square ledger accounting remain private).

## Project Needs & How You Can Help
- **3D Scanning & Printing:** Help capture or clean `.STL` / `.OBJ` / `.STEP` Scans of surplus housings, clips, and connectors (`scans/`), or test-print prototype shells/holders/mounts (`enclosure/`).
- **Spare / Extra Surplus Bench Gear:** Decommissioned surplus hardware, meters, logic analyzers, bus emulators, or bench supplies for non-clinical lab testing (`docs/BENCH_INSTRUMENTATION.md`).
- **Ideas & User / Community Stories:** Practical workflows, pain points, log/diagnostic tool ideas, and community perspectives—shared via GitHub Issues/Discussions or notes without exposing private medical/personal records.

## Environment & Paths
- Local repo: `D:\Downloads\HeartMate3-Battery-repo-starter\HeartMate3-Battery` on branch `main` (`origin/main`).
- Shell & tools: PowerShell with Git CLI and Python + Pillow (`PIL`) for image resizing/EXIF stripping.
- £Connectors & baseline: Standard `XT60`, `USB-C PD` (capped at `65W` / `~3.8A` for `4S1P Samsung INR21700-50G`), `4-pin JST-GH / Grove I2C`, and `UART` only; `0°C‑45°C` NTC charge gating, `60°C` hardware cutoff, `50%` SoC aux phone floor, and 3-layer hardware protection.

## Where to Find Info & How to Write
- **Live specs, structure, `BOM.csv`, and `[ ]` tasks:** Check the repo `.md` files and the `HM3-Battery-Research Live Repo` sheet tabs.
- **Locked ADRs, retired ideas & backstory:** Check `OpenHeart — Decisions & Lab Log` and `OpenHeart — project Background & Reference Wiki` in the `OpenHeart Battery` notebook.
- **Bench logging & checklists:** The Git commit log is the sole bench log—do not add bottom-of-doc changelogs, keep personal receipts/accounting private, and do not flip `- [ ]` to `- [x]` or guess unverified measurements.
- **Images:** Keep all photos in root `images/` named `device_subject_detail_number.jpg` (~1600 px wide, JPEG q=80, zero GPS/EXIF). Remind if a step adds a new image.

## Single-Command Commit & Push
```powershell
git add -A; git commit -m "<short summary>" -m "<detailed description>"; git push origin main
```
