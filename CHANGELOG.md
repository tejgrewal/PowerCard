# Changelog

All notable changes to this project will be documented in this file.
This project doesn't yet follow a formal versioning scheme (it's pre-release hardware) — dates are used until a v1.0 hardware release is tagged.

## [Unreleased]

### Changed
- Updated project status from "early preview" to "validated, working design" per designer confirmation that the fabricated board operates as intended (wireless + solar charging via the LTC4124's ACIN/DCIN inputs, and the LTC3246 5V fixed output stage).
- Reframed documentation from "known gaps / don't build yet" to "in-progress publication items" (schematic, USB-C daughter board files, stack thickness measurements) — the design works, these are documentation/publication tasks, not open engineering questions.
- Softened SAFETY.md to general good-practice guidance for lithium pouch cells and this design's charging inputs, rather than unresolved-risk framing.

### Added
- Initial public repository structure.
- `PCB1` main-board Gerbers and Excellon drill file, as fabricated (Altium Designer 26.3.0, project "CC Solar", fab data generated 2026-07-20).
- Fab reports (`.REP`, `.EXTREP`, `.DRR`) for the main board.
- Board photos (front/solar side, back/electronics side).
- Preview `BOM.md` covering `U1`–`U3`, passives, LED, and switch, sourced from the designer's Digi-Key parts list.
- `SAFETY.md` covering battery, wireless-charging, and solar-input safety considerations.
- `README.md` describing the overall architecture and the known documentation gaps.

### Known gaps (tracked, not yet resolved)
- Schematics not yet published.
- USB-C output daughter board files not yet added.
- Board/stack thickness measurements not yet documented.

See the README's [Roadmap](README.md#roadmap) for what's planned next.