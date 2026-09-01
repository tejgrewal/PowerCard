# PCB1 — Main Card Board

This is the main card-shaped PCB: wireless-charging receiver, boost/output regulator, battery connection, status LED, and pushbutton, on an 85.0 × 54.05 mm outline (ISO/IEC 7810 ID-1 credit-card footprint).

## Contents

- [`gerbers/`](gerbers/) — RS-274X Gerber layers + Excellon (`.TXT`) drill file, exactly as generated for fabrication (Altium Designer 26.3.0, project name "CC Solar", generated 2026-07-20). Also includes the Altium aperture files (`.apr`, `.APR_LIB`) and layer-pair export (`.LDP`) that were bundled with the fab export.
- [`../fab-outputs/`](../fab-outputs/) — the fab/drill reports (`.REP`, `.EXTREP`, `.DRR`) generated alongside the Gerbers, useful for a quick sanity check of layer count, drill sizes, and aperture usage without opening a Gerber viewer.

## Layer map

| File | Layer |
|---|---|
| `PCB1.GTL` | Top copper |
| `PCB1.GBL` | Bottom copper |
| `PCB1.GTO` | Top silkscreen |
| `PCB1.GBO` | Bottom silkscreen |
| `PCB1.GTS` | Top soldermask |
| `PCB1.GBS` | Bottom soldermask |
| `PCB1.GTP` | Top paste |
| `PCB1.GBP` | Bottom paste |
| `PCB1.GM` | Board outline / profile |
| `PCB1.GM9` | Board shape (mechanical) |
| `PCB1.TXT` | Excellon drill file (metric, leading zeros) — 49× Ø0.20 mm, 1× Ø0.45 mm, 2× Ø1.0 mm, all plated |

## Viewing the Gerbers

Any Gerber viewer will work — for a quick browser-based look without installing anything, try [Tracespace](https://tracespace.io/view/) or [GerbLook](http://www.gerblook.org/); for a full-featured desktop viewer, [KiCad's Gerber Viewer](https://www.kicad.org/) (free) or your fab's own viewer both work well.

## What's not here yet

Schematic source and native Altium PCB source (`.PcbDoc`/`.SchDoc`) are still being prepared for publication — see the [top-level README's Roadmap](../../README.md#roadmap). The board itself is fabricated and confirmed working.
