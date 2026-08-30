# Bill of Materials — Main Board `PCB1`

Parts list for the fabricated and validated main board, as supplied by the designer (Digi-Key part numbers). A schematic with net-level cross-referencing is in progress — see [`hardware/schematics/`](hardware/schematics/).

| Ref Des | Digi-Key Part Number | Description (from datasheet) | Qty Ordered |
|---|---|---|---|
| U1 | `505-LTC4124EV#TRMPBFCT-ND` | Analog Devices **LTC4124** — 100 mA wireless Li‑Ion battery charger with PowerPath control, low-battery disconnect, pin-selectable charge current/voltage. 12-lead 2×2 mm LQFN. Accepts power on two separate pins: **ACIN** (wireless coil LC tank) and **DCIN** (direct DC input — used here for the solar film). | 3 |
| U2 | `732-760308105214-ND` | FPC/board-to-board connector (mates to the USB‑C output daughter board over `J1`). | 2 |
| U3 | `LTC3246MPMSE#PBF-ND` | Analog Devices/Linear Technology **LTC3246** — inductor-less switched-capacitor buck-boost DC/DC converter with integrated watchdog timer; configured for a fixed 5 V output feeding the USB‑C daughter board. Confirmed working at 5V fixed output by the designer. "M" temp grade, MSOP-16 (MSE) w/ exposed pad. | 3 |
| C1 | `399-C0805C476M9PACTUCT-ND` | 47 µF, 0805 ceramic capacitor. | 10 |
| C2 | `399-C0805C104K5RACTUCT-ND` | 0.1 µF, 0805 ceramic capacitor. | 10 |
| C3 | `399-C0603C105K4PACTUCT-ND` | 1 µF, 0603 ceramic capacitor. | 10 |
| C4 | `490-4520-1-ND` | Ceramic capacitor (Panasonic). | 10 |
| C5 | `399-C0603C105K3PACTUCT-ND` | 1 µF, 0603 ceramic capacitor (different voltage rating than C3). | 10 |
| C6 | `490-7316-1-ND` | Ceramic capacitor (Panasonic). | 10 |
| D1 | `160-LTST-C190GKTCT-ND` | Status LED (Lite-On LTST-C190G family — green). | 10 |
| SW1 | `P19888CT-ND` | Tactile pushbutton switch. | 5 |
| R1 | `YAG4565CT-ND` | Resistor (value not specified in source list — confirm from schematic once published). | 10 |

### Not in the current parts list, but present in the physical design

| Item | Notes |
|---|---|
| Battery (B1) | 1 mm-thick LiPo pouch cell, printed marking `HZ 954750`, 3.7 V nominal, 180 mAh, sourced from [battery-vats.sell.everychina.com](https://battery-vats.sell.everychina.com/). No Digi-Key/distributor part number — see [`SAFETY.md`](SAFETY.md) regarding sourcing generic thin cells. |
| Solar film | PowerFilm **SP4.2-37** — 92 mW / 4.2 V / 22 mA (full sun), 84 × 37 mm active area, ~0.2 mm thick flexible amorphous-silicon module. Digi-Key/Mouser stock this part; add its part number here once confirmed. |
| Wireless charging coil | On-board copper spiral (visible in the board photo) — part of the PCB itself, not a discrete BOM line. |
| USB‑C connector | Lives on the separate 0.8 mm ENIG daughter board, not on `PCB1` — its BOM should be tracked in `hardware/usbc-output-board/` once added. |

### Open items for the next BOM revision

- **R1 value/tolerance** — not yet recorded here; add once the schematic is published (likely part of the DCIN input path from the solar film, given the LTC4124's DCIN/VCC/BAT 6V absolute max vs. the SP4.2-37's ~6.5V open-circuit voltage — worth a quick note in the schematic once it's up, for anyone else building this).
- Digi-Key part numbers here were transcribed from the designer's notes — worth a quick double-check against Digi-Key's catalog before ordering in bulk, as usual.