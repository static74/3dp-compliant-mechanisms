---
name: 3dp-compliant-mechanisms
description: Design compliant mechanisms, snap-fits, flexing joints and tolerance-free interfaces for FDM 3D-printed parts, following Slant 3D's design-for-any-printer method. Use whenever a user is designing printed parts that must fit, join, snap, latch, click, clip, hinge-free flex, press together, or hold a lid, cap, plug, pin, peg, tongue, slot, dovetail, spring or detent, even if they only say "make these two parts connect", "the lid is too loose/tight", "it fits on my printer but not his", or ask for a print-in-place latch or spring-loaded button. Also use when choosing between a printed spring and a metal spring, capturing a spring in a print, or when a fit depends on filament, nozzle or slicer settings. Covers geometry with provenance-tagged dimensions, print orientation, CAD steps and tuning.
---

# 3D-printed compliant mechanisms and interfaces

The thesis, from Slant 3D: never tune clearances to a printer. Fit drifts with filament colour, material, machine, nozzle and layer height. Design geometry that self-centres, wedges or flexes so the same file works on every printer. Every mechanism here applies that rule.

## Workflow
1. Read `references/fundamentals.md` once per session. It holds the orientation rule, allowable strains, clearance tables, first-layer and overhang rules, and the provenance tags (`[video]`, `[measured]`, `[source]`, `[judgment]`) that every number carries.
2. Pick the mechanism with the table below, or confirm the user's choice against its "Avoid when" line.
3. Open only that family's reference file. Follow its Geometry, Print, Model it and Tune it sections.
4. If the mechanism is spring-loaded, also read `references/spring-loaded.md` and ask (or decide, if the user gave enough context) printed spring vs metal spring. A metal spring always needs one of the two capture methods in `references/spring-capture.md`.
5. Deliver in the format in fundamentals §12: mechanism and why, parameter table with tags, orientation, CAD steps, tuning note. Flag every `[judgment]` value as needing one test print.
6. Before you send, close the geometry: every stacked dimension adds up (cavity depth, barb span versus counterbore, slot plus two prongs equals the split-zone diameter, nub position used as the lever length), every strain uses the right lever and the right factor, and every first layer has a footprint. The eval graders check this, and so will the engineer.

## Selection table
| User needs | Mechanism | File |
|---|---|---|
| Lid, cap, plug or insert that fits a printed opening on any printer | grip-fin lid (default for PETG/ASA or lids opened often); side springs with a nub-in-dimple for PLA lids that stay closed (the arm relaxes when seated, so no creep); perforated plug for easy-open friction; press-fit only if permanent | `compliant-lids.md` |
| Lid that must click and hold a load, ~2 mm engagement | internal spring latch (spring-loaded) | `compliant-lids.md` §E + `spring-loaded.md` |
| Two parts joined tool-free, separable, kit-style | bi-directional locking tab "Snap In" (Slant's recommendation) | `snap-fits.md` |
| Two parts clipped by a third small piece | S-bracket (strongest) or C-clamp clip (easiest) | `snap-fits.md` |
| Detent that pops in and out | forked detent pin | `snap-fits.md` |
| Edge-to-edge panels, large prints in sections | flexible T-slot (default), eye slot if the tongue prints face-down, grip-fin eye for mixed printers | `tongue-and-slot.md` |
| Alignment pin/peg between glued or pressed parts | horizontal: diamond peg or keyhole pin; vertical: cruciform or fluted micro-slot pin | `pins-and-holes.md` |
| Side-loaded vertical pin keeps snapping | fluted pin with internal cross and 0.2 mm micro-slots | `pins-and-holes.md` |
| Spring-loaded plunger, button, detent, latch, pogo | printed serpentine/cantilever spring (travel ≤ ~2 mm) or metal compression spring (more travel/force) | `spring-loaded.md` + `spring-capture.md` |
| Parts will be glued | undercut pocket grid, glue patch, relief bead, injection channel | `glue-features.md` |
| Hole prints undersized or sagging | polyhole / teardrop | `fundamentals.md` §9, §11 |
| Thin feature needs wall-dense infill without slicer changes | 0.2 mm micro-slots (unqualified; test against a solid control) | `fundamentals.md` §10 |

## Choosing on your own
When the user describes a fit problem without naming a mechanism, prefer, in order: a flexing feature over a rigid clearance; redundancy (many fins) over one spring; in-plane flexure over anything built vertically; a 45° chamfer over a fillet on downward faces; PETG/ASA over PLA for anything that stays preloaded. Say which mechanism you chose and why in one sentence before the parameters.

## Spring option rule (binding project requirement)
Any mechanism with a spring offers both a printed spring and a metal spring. For the metal spring, the plunger or latch the spring pushes on must be retained by one of exactly two methods, both specified in `spring-capture.md`: (A) one-way barbed fins or ears on the plunger that snap into the bore from outside and cannot be pushed back out, or (B) a slicer pause at the cavity-roof layer so the spring is placed mid-print and sealed in. This is a requirement of the organisation that owns this skill, not a physics claim: a screwed or press-fit rear cap with a plunger collar is also a valid retainer, and you may mention it, but deliver A or B. State which one you used and why.

## Adding a mechanism
Copy `references/_template.md`, fill every section with tagged numbers, add one row above, add an eval case under `evals/`, and log it in the repo's `docs/decisions.md`. Keep this file under 300 lines; knowledge lives in the references.

## Where the sources live
References cite `docs/research/*.md`. Those files are in the repository one directory above this skill (`../docs/research/`), not in the skill folder. They hold every URL and derivation; read them only when a user challenges a number.

## Scope limits
These are FDM numbers (0.4 mm nozzle, 0.2 mm layers). Resin and MJF have different clearance and strain rules. Strain values are derived from datasheets with moulded-plastic snap-fit rules, not measured on printed beams; treat them as starting points.
