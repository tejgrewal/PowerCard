# PowerCard — Credit‑Card‑Sized Solar / Wireless Power Bank

**Status:** ✅ Validated design — main board (`PCB1`) has been fabricated and confirmed working by the designer. Schematics, full BOM, and enclosure/3D files are being prepared for publication (see [Roadmap](#roadmap)).

PowerCard is an open-hardware power bank designed to fit in a wallet: the main board footprint matches an **ISO/IEC 7810 ID‑1 card (85.6 × 54 mm)**, and the target stack-up is roughly the thickness of two stacked credit cards. It charges wirelessly (Qi-style coil) or from an integrated flexible solar film, stores energy in an ultra-thin 1 mm LiPo pouch cell, and outputs regulated 5 V over USB‑C through a small companion board.

![Front of the PCB1 board — flexible solar film side](docs/images/board-front-solar-side.jpg)
![Back of the PCB1 board — wireless coil, battery and charge electronics](docs/images/board-back-electronics-side.jpg)

> The photos above show the fabricated `PCB1` main board on an ESD mat, ruler for scale, populated with the wireless-charging and battery-management electronics, mated to a 1 mm LiPo pouch cell and a PowerFilm flexible solar module.

---

## How it works

```
                 ┌────────────────────────────┐
  ☀ Solar film   │                            │
  (PowerFilm     │                            │
   SP4.2-37)     │                            │
        \        │        PCB1                │
         \___?___│   (main card board)        │
                 │                            │      FPC       ┌──────────────────┐
  🔵 Qi coil ─────┤  U1  LTC4124               │────connector───▶  USB-C output board │──▶ 5V USB-C
  (on-board)     │  (wireless Li-Ion charger) │     (J1)       │  (0.8 mm, ENIG)    │
                 │                            │                │  U3 LTC3246 boost  │
                 │  B1  1 mm LiPo pouch cell  │                └──────────────────┘
                 │  (180 mAh, "954750")       │
                 │  SW1 pushbutton, D1 status │
                 │  LED, U2 FPC connector     │
                 └────────────────────────────┘
```

* **Input 1 — Wireless charging:** an on-board coil feeds **U1, an Analog Devices/Linear Technology LTC4124** — a 100 mA wireless Li‑Ion charger with integrated PowerPath control and low-battery disconnect. It charges the cell from an external Qi-style/resonant transmitter coil held against the card, via the IC's **ACIN** pin (an internal diode routes AC-tank power to VCC).
* **Input 2 — Solar:** a **PowerFilm SP4.2‑37** flexible amorphous-silicon film (92 mW, 4.2 V / 22 mA in full sun, ~0.2 mm thick, up to ~6.5 V open-circuit) is laminated to the opposite face of the card, feeding the LTC4124's **DCIN** pin — the IC's dedicated direct-DC input, separate from the coil/ACIN path. Confirmed working by the designer.
* **Storage:** a **1 mm-thick, 180 mAh LiPo pouch cell** (marked `HZ 954750`, 3.7 V nominal), sourced from a generic overseas cell vendor. See [`SAFETY.md`](SAFETY.md) for general handling guidance — standard good practice for any lithium pouch cell project.
* **Output:** **U3, an LTC3246MPMSE** switched-capacitor (inductor-less) buck-boost converter, configured for a fixed regulated 5 V rail, feeding a separately fabricated 0.8 mm ENIG USB‑C output daughter board over an FPC connector (`J1`/`U2`). Confirmed working at 5V fixed output by the designer.
* **UI:** one status LED (`D1`) and one tactile pushbutton (`SW1`).

## Repository layout

```
PowerCard/
├── README.md                  ← you are here
├── SAFETY.md                  ← battery & solar safety notes — read before building
├── BOM.md                     ← partial bill of materials (as supplied so far)
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
│   ├── usbc-output-board/     ← placeholder — daughter board files to be added
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
| Board thickness | *Not encoded in the Gerber set — confirm with your fab. The mating USB‑C daughter board is specified as 0.8 mm ENIG; the main board's thickness should be chosen to hit your target overall card thickness once the 1 mm cell is stacked in.* |

Full Gerber/drill files: [`hardware/pcb1-main-board/gerbers/`](hardware/pcb1-main-board/gerbers/)

## Bill of materials

A partial BOM (as supplied by the designer, Digi-Key part numbers) is in [`BOM.md`](BOM.md). **Schematics have not been published yet** — treat reference designators as provisional until a schematic is added and cross-checked against the silkscreen.

## What's still being published

The design itself is validated and working. The following documentation/files are still being prepared:

1. **Schematic** — not yet published. The BOM and photos document the working design, but a schematic will make it easier for others to build from scratch.
2. **USB‑C output board files** — the main board mates to it via the `J1` FPC connector; its own Gerbers/BOM will be added separately.
3. **Board/stack thickness measurements** — "thin as two credit cards" is the design target; exact per-layer and total assembled thickness will be documented once measured/finalized.
4. **Full, schematic-cross-checked BOM** — the current BOM (below) is accurate to the fabricated board but hasn't yet been tied to net names in a published schematic.

If you're the designer, treat this as the top of the roadmap. If you're a visitor building from this repo in the meantime, the photos + BOM are your best reference until the schematic lands — see [`docs/hardware-overview.md`](docs/hardware-overview.md).

If you're the designer, treat this list as the top of the roadmap. If you're a visitor, please don't fabricate/assemble a battery-powered board from an incomplete design.

## Roadmap

- [ ] Publish schematics (main board + USB‑C output board)
- [ ] Publish complete BOM cross-checked against schematic net names
- [ ] Add USB‑C output daughter board Gerbers
- [ ] Measure and document per-layer and total stack thickness
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