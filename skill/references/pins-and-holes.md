# Pins, pegs and holes

**Family:** press-fit locators between separately printed parts
**Use when:** two parts need alignment and friction retention, often with glue; or a pin must survive side loads.
**Avoid when:** a rigid round press fit is expected to hold on its own. Allowable interference (≈0.06–0.12 mm on a 6 mm PLA pin) is below printer accuracy, so round pins are either loose or crack the hole `[source: Bayer annular limit]`.
**Source:** Slant 3D joints guide Parts A1, D, E.

## Horizontal pins (pin axis in the bed plane) `[video]`
Layers run along the pin, so it is strong in bending.
| Feature | Default | Tag |
|---|---|---|
| Diamond peg (A1) | square peg rotated 45° so the mating hole has no overhang; 6–8 mm across, 6–8 mm long `[judgment]`; gap 0.15–0.20/side | `[video; sizes judgment]` |
| Pin tip | 45° chamfer, 0.5–1.0 mm (a chamfer is a constant overhang; a fillet goes to infinite overhang) | `[video; size judgment]` |
| Round hole with axis horizontal | teardrop, 45° flats (90° apex), or truncated with ≤ 3 mm flat; offset the hole +0.2 mm for sag | `[video + source: Hubs]` |
| Keyhole pin (D2) | round pin with triangular fins top and bottom (arrowhead section) so it prints in any orientation without support; side walls do the fit, fins carry tension | `[video]` |
| Slot tab (D3) | replace the round pin with a rectangular tab into a rectangular slot, chamfered; only the slot sides interface | `[video]` |
| Self-centering wedge tab (D4) | tab tapered 1–2° along its length so the top is narrower than the slot mouth and the base wider; use two tabs slightly offset to self-centre | `[video; angle source: Siraya]` |
| Forked detent pin (D5) | see snap-fits.md | |

## Vertical pins (pin axis in Z) `[video E2]`
Fail in interlayer shear at the base, so keep them short and fat.
| Parameter | Default | Tag |
|---|---|---|
| Diameter | ≥ 5 mm (below that, fillet the base and raise wall density with micro-slots or 100 % infill; see fundamentals §10 caveat) | `[source: Hubs]` |
| Height | as short as possible, L/d ≤ 1.5 | `[video; ratio judgment]` |
| Hole oversize | 0.25 mm diametral; up to 0.5 for ABS/ASA/nylon | `[video]` |
| Hole lead-in | fillet or 45° chamfer funnel, 0.5–1.0 mm | `[video; size judgment]` |
| Pin base fillet | 0.5–1.0 mm, matching the hole lead-in | `[video + source: Bayer R/t 0.6]` |
| Pin top | round or 45° chamfer so it self-locates | `[video]` |
| Draft | 1.5° (1–2°): base wider than the hole, tip narrower, so it wedges | `[video, Shapr3D panel]` |
| Vertical hole correction | +0.1–0.2 mm or polyhole (fundamentals §11) | `[source: nophead]` |

### Cruciform pin (E3) `[video]`
Plus-shaped section instead of a cylinder: ribs run in line with the load, and the cross wears in on repeated insertion so the outer walls never bind. Height 10 mm, draft 1.5° `[video panel]`; arms 1.35–2.0 mm (3–4 perimeters) so each arm is solid wall `[source: Prusa KB; video slicer view]`. Matching plus-shaped hole with lead-in chamfer and 0.25 mm diametral clearance.

### Fluted pin with internal cross and micro-slots (E4) `[video]` (Slant's final design)
Cylinder whose rim is scalloped with ~16 half-round flutes `[measured estimate]`, an internal cross, and 0.2 mm slots that run from the tip through the base and 2–5 mm into the body so the pin prints as stacked walls rather than infill (fundamentals §10; the slots remain voids and the technique is unqualified until compared with a solid control). Maximum material at the outer edge where cracks start. Same hole rules as E2.

## Model it (vertical pin)
1. Sketch the pin section (circle, plus, or fluted circle) on the top face.
2. Extrude 1-sided, height ≤ 1.5·d, draft 1.5°.
3. Fillet the base 0.5–1 mm; fillet or chamfer the top.
4. On the mating part, offset the section +0.125 mm per side (0.25 diametral), cut, add a 0.5–1 mm lead-in chamfer.
5. Optional: sketch 0.2 mm wide slots across the pin section, spaced ~1 mm, extrude-cut from the tip to 2–5 mm below the base.

## Tune it
Loose: widen the cross arms or raise the draft so the base interferes more (contact size is what sets grip); wear-in only conforms a tight fit, it never tightens a loose one. Do not shrink the hole below 0.25 mm diametral. Cracks the hole: add draft, reduce height, chamfer the hole mouth. Pin breaks: shorten, fatten, fillet the base, or print it horizontal.

## Failure modes
- Hole oblong or sagging (horizontal): use teardrop or diamond.
- Pin shears at base (vertical): short, fat, filleted, or wall-dense (micro-slots, tested against a solid control).
- Round peg printed horizontally snaps: it is in-plane with layers only along one axis; use a square/diamond peg.
