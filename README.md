# 3dp-compliant-mechanisms

A Claude skill for designing compliant mechanisms, snap-fits, flexing joints and tolerance-free interfaces for FDM 3D printing, built on Slant 3D's "design for any printer" method.

The skill lives in [`skill/`](skill/). `skill/SKILL.md` routes to one reference file per mechanism family:

| File | Covers |
|---|---|
| `fundamentals.md` | orientation rule, allowable strain by material, clearance tables, first layer, overhangs, 0.2 mm micro-slots, polyholes |
| `compliant-lids.md` | press-fit, perforated plug, side springs, grip fins, spring latches |
| `snap-fits.md` | C-clamp clip, S-bracket, bi-directional locking tab, forked detent pin |
| `tongue-and-slot.md` | tongue, T-slot, flexible (leaf-spring) T-slot, eye slot, grip-fin eye slot, dovetail |
| `pins-and-holes.md` | diamond peg, keyhole pin, wedge tab, vertical pins, cruciform pin, fluted micro-slot pin |
| `spring-loaded.md` | printed vs metal spring decision, printed leaf sizing, stock spring table, plunger body |
| `spring-capture.md` | one-way barbed plunger; slicer-pause spring capture (PrusaSlicer, Cura, Bambu) |
| `glue-features.md` | undercut pocket grid, glue patches, relief bead, injection channels |

Every number carries a provenance tag: `[video]` stated in a Slant 3D video, `[measured]` read from frames against a known dimension, `[source: URL]` published guide or datasheet, `[judgment]` untested engineering judgment.

## Install
```bash
ln -s "$(pwd)/skill" ~/.claude/skills/3dp-compliant-mechanisms
```

## Test
```bash
claude plugin eval skill --allow-tools Write,Edit,Bash
```

## Sources
Slant 3D "Design Compliant Lids for Perfect Tolerance Every Time" and "Ultimate Guide to Connecting 3D Printed Parts", plus Bayer/BASF snap-fit guides, Prusa Knowledge Base, PrusaSlicer source, Lee Spring catalog, Polymaker/Prusament datasheets and Akaki Kuumeri's flexure talk. Full reports with URLs are in [`docs/research/`](docs/research/). See `docs/sources.md`.

## Adding a mechanism
See `AGENTS.md`.
