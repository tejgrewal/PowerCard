# Safety Notes

This project uses a lithium-polymer pouch cell, a wireless-power receiver, and a flexible solar film in a thin, flexible, wallet-carried card. The design has been fabricated and validated by the designer. This document covers general good-practice handling for lithium pouch cells and this design's charging inputs — worth reading once regardless of how validated a design is, since it's really about how *you* handle a cell day to day, not a doubt about the design itself.

## Battery handling

- The cell used (`HZ 954750`, 1 mm thick, 180 mAh, 3.7 V) is an ultra-thin pouch cell. As with any thin pouch cell, avoid flexing, puncturing, or crushing the assembled card near the battery, and don't laminate/seal the pouch in a way that prevents it from venting if it ever needs to.
- Physically inspect cells before first use: swelling, punctures, discoloration, or a chemical smell are all reasons to set that cell aside.
- Charge new prototypes on a fireproof surface, away from flammable materials, for the first several cycles until you're familiar with how the board behaves.

## Wireless charging and solar input

- The LTC4124 accepts power from a matched wireless-power transmitter coil on its **ACIN** pin, and from the solar film on its **DCIN** pin — two separate, intended input paths on the same charger IC. Use a transmitter intended for low-power (sub-1 W to few-W) Qi-style or resonant wireless charging.
- Worth a quick check once the schematic is published (mostly for anyone else building this from the repo): the LTC4124's DCIN/VCC/BAT absolute maximum rating is 6 V, and the SP4.2‑37's open-circuit voltage can reach roughly 6.5 V in full sun with no load. Documenting how that margin is handled (likely via `R1`) will help other builders trust the design without having to re-derive it themselves.

## General handling

- Treat the assembled card the same way you'd treat any other small lithium battery project: no charging inside a pocket, bag, or under a pillow; no charging near paper/fabric.
- If a cell ever swells, gets hot, or smells strange, disconnect it, move it to a safe non-flammable area, and let it fully discharge/cool before disposal via a battery recycling program — don't throw it in household trash.

## Contributing safety improvements

If you spot something worth adding here as the design evolves, please open an issue (see [`CONTRIBUTING.md`](CONTRIBUTING.md)) — safety documentation for an open-hardware project only works if it stays current.