# PHANTOM GRID

> *Offline-first. Air-gapped. Encrypted. Built for the field.*

Phantom Grid is a series of purpose-built handheld devices engineered for those who operate outside the comfort of connectivity. No Wi-Fi. No cloud sync. No IP assignment. Every hardware and firmware decision is governed by a single principle: **security first, convenience never.**

https://phantom-grid.netlify.app - our site :0

---

## Series

| ID | Name | Description |
|----|------|-------------|
| **S** | Survival | Bare minimum. Maximum efficiency. Built to run when nothing else does. |
| **T** | Tactical | Feature-packed, encrypted, hardened. Heavy-duty field use. |
| **X** | Experimental | Highly specialised. Each unit unique. Not for general deployment. |
| **C** | Cyber | Fully off-grid. Offensive posture. Maximum resource load. |

---

## Current Build — T-V.1

The first Tactical series device. Dual-panel, hinged form factor with three independent displays, local sensor data, GPS, and an air-gapped file archive terminal.

### Architecture

- **Dual ESP32-C6 SuperMini** — one per side, connected via 4-wire UART hinge link
- **Left side** — Tactical Overwatch Panel (OLEDs, 5-way nav, GPS, temperature, moisture, battery)
- **Right side** — Archive Command Terminal (ILI9341 TFT, microSD, tactile buttons)
- **Power** — LiPo 2000–2500mAh → TP4056 (dual protection) → 3.3V buck converter → shared rail via hinge

### Displays

| Display | Role | Interface |
|---------|------|-----------|
| 0.91" OLED 128×32 | Battery, time, date | I²C |
| 1.5" OLED 128×128 | GPS, temperature, sensor data | I²C via TCA9548A |
| 2.4" TFT ILI9341 | File browser, archive terminal | SPI |

### Storage

Files are loaded onto the microSD card by **physically removing it**, writing via USB adapter on a separate machine, and reinserting. No cloud sync. No Wi-Fi. No detectable radio signature. By design.

---

## Build Phases

- [x] **Phase 1** — Architecture & Pinout
- [x] **Phase 2** — Breadboard Prototype
- [x] **Phase 3** — Firmware Foundation
- [x] **Phase 4** — Feature Layer
- [x] **Phase 5** — Firmware Hardening
- [ ] **Phase 6** — Physical Build

 (working on getting the parts to build the first prototype now)

---

## Firmware Protection (Phase 5)

- Strip all debug symbols, aggressive optimisation (`-O2/-O3`)
- Obfuscator-LLVM control flow mangling
- CRC/hash self-check on boot — halts if tampered
- Chip ID binding — binds to first chip it runs on, cloning breaks it
- Sensitive logic derived at runtime, never stored plainly in binary
- Binary-only distribution with checksum and signature

---

## Repository Structure

```
phantom-grid/
├── site/               # Project website (Netlify)
│   ├── index.html
│   ├── bom.html
│   └── trifold.html
├── docs/               # Reference documents
│   ├── Phantom_Grid_T-V1_Reference.docx
│   └── Phantom_Grid_T-V1_Session_Summary.md
├── firmware/
│   ├── left/           # Left ESP32 — Tactical Overwatch Panel
│   └── right/          # Right ESP32 — Archive Command Terminal
└── hardware/
    ├── pinout/
    └── schematics/
```

---

## Estimated Build Cost

**~£43–80** depending on component sourcing. All parts sourced from AliExpress. Full BOM available in `site/bom.html`.

---

## Licensing

| What | Licence |
|------|---------|
| PCB files, enclosure, skeleton firmware | [CERN OHL-S v2](./LICENSE) — open hardware, strongly reciprocal |
| Full feature firmware | Proprietary — binary only, never released |

The skeleton code and hardware files are open — you can use, modify and build on them freely, but any changes you distribute must be released under the same licence. The full firmware powering commercial units is proprietary and protected. It is never distributed in source form.

---

## Licensing

This project uses a dual licensing model:

| What | Licence | Details |
|------|---------|---------|
| PCB files, enclosure, skeleton firmware | **CERN-OHL-S v2** | Open hardware — modifications must be released under the same licence |
| Full feature firmware | **Proprietary** | Never released — binary only, chip-bound, encrypted |

The open skeleton gives you everything you need to understand how the device is wired and structured. The full firmware with all features ships only with commercially built units and is protected by hardware-level encryption and chip binding. You are free to build your own version using the open source materials — you cannot take the commercial firmware.

---

*PG-T-V.1 / REV.002 / ENCRYPTED / AIR-GAPPED*
