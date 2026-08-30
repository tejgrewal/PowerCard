# PowerCard — Credit‑Card‑Sized Solar / Wireless Power Bank

**Status:** ✅ Validated design — main board (`PCB1`) has been fabricated and confirmed working by the designer. Schematics, full BOM, and enclosure/3D files are being prepared for publication (see [Roadmap](#roadmap)).

PowerCard is an open-hardware power bank designed to fit in a wallet: the board footprint matches an **ISO/IEC 7810 ID‑1 card (85.6 × 54 mm)**, and the target stack-up is roughly the thickness of two stacked credit cards. Everything lives on a single board (`PCB1`): it charges wirelessly (Qi-style coil) or from an integrated flexible solar film, stores energy in an ultra-thin 1 mm LiPo pouch cell, and outputs regulated 5 V directly over USB‑C.

![Front of the PCB1 board — flexible solar film side](docs/images/board-front-solar-side.jpg)
![Back of the PCB1 board — wireless coil, battery and charge electronics](docs/images/board-back-electronics-side.jpg)

> The photos above show the fabricated `PCB1` board on an ESD mat, ruler for scale, populated with the wireless-charging, solar-charging, and boost/output electronics, mated to a 1 mm LiPo pouch cell and a PowerFilm flexible solar module.

---

## How it works

```
                 ┌─────────────────────────────────────┐
  ☀ Solar film   │                                     │
  (PowerFilm     │                                     │
   SP4.2-37) ────┤  U1  LTC4124                         │
                 │  (wireless Li-Ion charger,           │
  🔵 Qi coil ─────┤   ACIN + DCIN inputs)                │
  (on-board)     │                                     │
                 │  B1  1 mm LiPo pouch cell            │
                 │  (180 mAh, "954750")                 │
                 │                                     │
                 │  U3  LTC3246 (fixed 5V boost) ────────┼──▶ 5V USB-C
                 │                                     │
                 │  SW1 pushbutton, D1 status LED       │
                 │  J1 / U2  on-board FPC connector      │
                 └─────────────────────────────────────┘
                        single board — PCB1
```

* **Input 1 — Wireless charging:** an on-board coil feeds **U1, an Analog Devices/Linear Technology LTC4124** — a 100 mA wireless Li‑Ion charger with integrated PowerPath control and low-battery disconnect. It charges the cell from an external Qi-style/resonant transmitter coil held against the card, via the IC's **ACIN** pin (an internal diode routes AC-tank power to VCC).
* **Input 2 — Solar:** a **PowerFilm SP4.2‑37** flexible amorphous-silicon film (92 mW, 4.2 V / 22 mA in full sun, ~0.2 mm thick, up to ~6.5 V open-circuit) is laminated to the same board, feeding the LTC4124's **DCIN** pin — the IC's dedicated direct-DC input, separate from the coil/ACIN path. Confirmed working by the designer.
* **Storage:** a **1 mm-thick, 180 mAh LiPo pouch cell** (marked `HZ 954750`, 3.7 V nominal), sourced from a generic overseas cell vendor. See [`SAFETY.md`](SAFETY.md) for general handling guidance — standard good practice for any lithium pouch cell project.
* **Output:** **U3, an LTC3246MPMSE** switched-capacitor (inductor-less) buck-boost converter, configured for a fixed regulated 5 V rail, feeding the USB‑C output connector directly on `PCB1`. Confirmed working at 5V fixed output by the designer.
* **UI:** one status LED (`D1`) and one tactile pushbutton (`SW1`).
* **On-board connector:** one FPC connector (`J1`, mating part `U2`) is present on the board — see [`BOM.md`](BOM.md) for the part number; its exact function will be documented once the schematic is published.

## Repository layout

```
PowerCard/
├── README.md                  ← you are here
├── SAFETY.md                  ← battery & solar safety notes — read before building
├── BOM.md                     ← bill of materials (as supplied so far)
├── CONTRIBUTING.md
├── CHANGELOG.md
├── LICENSE                    ← hardware license (CERN-OHL-S-2.0)
├── LICENSE-DOCS                ← documentation license (CC-BY-4.0)
├── docs/
│   └── images/                ← board photos
├── hardware/
│   ├── pcb1-main-board/
│   │   ├── gerbers/           ← RS-274X Gerbers + Excellon drill (as fabricated)
│   │   └── fab-outputs/       ← fab report (.REP), drill report (.DRR), extension map
│   └── schematics/            ← placeholder — schematics to be added
└── .github/                   ← issue templates
```

## Board specifications (as measured from the supplied Gerbers)

| Parameter | Value |
|---|---|
| Board outline | 85.0 mm × 54.05 mm (ID‑1 credit-card footprint) |
| Layers | 2 (Top + Bottom copper, top/bottom silkscreen, soldermask, paste) |
| Surface finish | ENIG (per designer) |
| Drills | 49× Ø0.20 mm, 1× Ø0.45 mm, 2× Ø1.0 mm (52 total, all plated) |
| CAD tool | Altium Designer 26.3.0, project "CC Solar" |
| Fab data generated | 2026‑07‑20 |
| Board thickness | *Not encoded in the Gerber set — confirm with your fab and document here once the target overall card thickness (with the 1 mm cell stacked in) is finalized.* |

Full Gerber/drill files: [`hardware/pcb1-main-board/gerbers/`](hardware/pcb1-main-board/gerbers/)

## Bill of materials

A BOM (as supplied by the designer, Digi-Key part numbers) is in [`BOM.md`](BOM.md). A schematic with net-level cross-referencing is in progress — see [`hardware/schematics/`](hardware/schematics/).

## What's still being published

The design itself is validated and working, on a single board. The following documentation/files are still being prepared:

1. **Schematic** — not yet published. The BOM and photos document the working design, but a schematic will make it easier for others to build from scratch, and will clarify what the on-board FPC connector (`J1`/`U2`) is used for.
2. **Board/stack thickness measurements** — "thin as two credit cards" is the design target; exact board thickness and total assembled thickness (with the 1 mm cell) will be documented once measured/finalized.
3. **Full, schematic-cross-checked BOM** — the current BOM (below) is accurate to the fabricated board but hasn't yet been tied to net names in a published schematic.

If you're the designer, treat this as the top of the roadmap. If you're a visitor building from this repo in the meantime, the photos + BOM are your best reference until the schematic lands — see [`docs/hardware-overview.md`](docs/hardware-overview.md).

## Roadmap

- [ ] Publish schematic
- [ ] Publish complete BOM cross-checked against schematic net names
- [ ] Document the on-board FPC connector's (`J1`) function
- [ ] Measure and document board and total assembled stack thickness
- [ ] Post assembly photos and a bring-up/test procedure
- [ ] Add STEP/3D models

## License

Hardware design files (Gerbers, and future schematics/PCB source) are released under the **CERN Open Hardware Licence Version 2 – Strongly Reciprocal (CERN-OHL-S-2.0)** — see [`LICENSE`](LICENSE).

Documentation (this README, `docs/`, etc.) is released under **Creative Commons Attribution 4.0 (CC-BY-4.0)** — see [`LICENSE-DOCS`](LICENSE-DOCS).

Referenced part numbers, datasheets, and manufacturer names (Analog Devices/Linear Technology, PowerFilm, Digi-Key, etc.) remain the property of their respective owners; this project simply documents how they are used together.

## Contributing

See [`CONTRIBUTING.md`](CONTRIBUTING.md). Bug reports, schematic reviews, and safety feedback are especially welcome while the design is in preview.

## Safety

See [`SAFETY.md`](SAFETY.md) for general handling guidance for the lithium-polymer pouch cell, wireless charging, and solar input — standard good practice for any small lithium battery project, regardless of how well-validated the design is.
