# Contributing to PowerCard

Thanks for taking an interest in this project — it's an early-stage, hobbyist open-hardware release, and outside eyes on the schematic, BOM, and safety approach are genuinely useful.

## Ways to help right now

Given the project's current state (see the README's [Roadmap](README.md#roadmap)), the most valuable contributions at this stage are:

1. **Schematic review**, once one is published — does the wiring match the BOM and photos?
2. **BOM verification** — confirming Digi-Key part numbers actually match the described parts, flagging obsolete/EOL parts, suggesting in-stock alternatives.
3. **Datasheet-informed design feedback** — e.g., confirming the LTC3246's output current fits your intended use, or the LTC4124's charge-current setting matches the battery's safe charge rate.
4. **Documentation fixes** — typos, unclear wording, missing units.
5. **General safety feedback** — see [`SAFETY.md`](SAFETY.md).

## Reporting issues

Please open a GitHub issue and include:
- What you were trying to do (build, review, simulate, etc.)
- Which file(s) you're referring to
- For safety-related issues, please say so explicitly in the title (e.g., `[safety] ...`) so they get prioritized

## Submitting changes

1. Fork the repo and create a branch for your change.
2. Keep hardware-file changes (Gerbers, schematics, footprints) and documentation changes in separate commits/PRs where possible, so reviewers can evaluate them independently.
3. If you're changing or adding to the BOM, please cite a source (datasheet, distributor page) for any new part number.
4. If your change affects battery charging, protection, or the solar/wireless input paths, please also update `SAFETY.md`.
5. Open a pull request describing what changed and why. Small, focused PRs are much easier to review than large ones.

## Design file formats

- PCB/schematic source: Altium Designer (the original design was created in Altium Designer 26.3.0). If you don't have access to Altium, you can still review/fabricate from the Gerber + Excellon drill files in `hardware/*/gerbers/`.
- Please don't commit binary CAD files without also exporting human-reviewable Gerbers/PDFs alongside them, so contributors without the exact CAD tool can still review changes.

## Code of conduct

Be respectful, assume good faith, and remember that some contributors here may be newer to hardware design or to lithium battery safety — explain your reasoning, don't just say "this is wrong."