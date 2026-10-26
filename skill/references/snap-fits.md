# Cantilever snap-fits: clips, brackets, locking tabs, detent forks

**Family:** snap-fit (separable, two or more printed parts pressed together)
**Use when:** two printed parts must join tool-free, hold under load, and optionally come apart again.
**Avoid when:** the part is PLA and must stay snapped under sustained strain for months (PLA creeps), or the beam would have to be built vertically in Z.
**Source:** Slant 3D "Ultimate Guide to Connecting 3D Printed Parts" (Part A clips, B6 locking tab, D5 forked pin); Bayer snap-fit guide; Hubs.

## How it works
A cantilever beam with a hook, bump or lip at its tip deflects over a mating edge during insertion and springs back into an undercut. The beam's thickness-to-length ratio sets travel and force; the two face angles set insertion force and whether it releases. Tolerance is absorbed by making the undercut deeper than the printer error.

## Shared geometry
| Parameter | Default | Range | Tag |
|---|---|---|---|
| Root thickness t | 1.8 mm (4 perimeters) | 1.35–2.7 | `[source: Hubs ≥1 mm; Prusa KB multiples]` |
| Tip thickness | 0.9 mm (taper to t/2) | ≥ 0.9 | `[source: Bayer taper]` |
| Width b | 6 mm | ≥ 5 | `[source: Hubs]` |
| Length L | solve L = √(y·t/(1.09·ε)) with tapered beam; PLA releasable at y=0.8, t=1.8 gives 10.5 mm | L/t 8–12 | `[source: Bayer]` |
| Undercut / hook depth y | 0.8 mm | 0.6–1.2 (must exceed gap + 0.2 mm print error) | `[source: Hubs; derived]` |
| Insertion angle α | 30° | 20–35° | `[source: Bayer]` |
| Return angle α′ permanent | 90° | ≥ 63° self-locks | `[source: BASF; derived]` |
| Return angle α′ releasable | 45° | 35–45° | `[source: Fictiv; derived]` |
| Root fillet | 0.6·t ≈ 1.1 mm | ≥ 0.38 | `[source: Bayer]` |
| Mating gap (sides of the beam/tab) | 0.3 mm | 0.25 PLA/PETG, 0.35–0.5 ABS/ASA | `[source: Fictiv, Qidi]` |

Worked example (PLA, releasable, copy for any tab): t 1.8→0.9, b 6, y 0.8, ε 1.2 % → L 10.5 mm, deflection force ≈ 8.5 N, insertion ≈ 13 N at α 30°, removal ≈ 26 N at α′ 45°. At α′ 90° it is permanent.

## Variants

### C-clamp clip (A4) `[video]`
Separate U-shaped clip with two hooked tines pressed into a rectangular slot; each tine latches into a pocket inside the part. Each tine takes half the total closing deflection. Print the clip flat (profile in XY). Easiest to use, least robust of the clips because both latches must catch.

### S-bracket (A3) `[video]`
Separate zig-zag strip; each part gets a matching slot, the S sits half in each and its hooked ends snap into small side pockets. Symmetric, so one pocket design repeats everywhere. "Compression" means the free length is 0.3–0.5 mm longer than the pocket spacing `[judgment]`. Strip 1.35–1.8 mm thick, ≥ 5 mm wide, bend radii ≥ 0.6·t, hooks per the shared table. Strongest and tightest of the Part A joints. Print flat.

### Bi-directional locking tab, "Snap In" (B6) `[video]` (Slant's recommendation)
Male: rectangular stem (~10 × 10 mm section on a 25 mm cube `[measured ±2]`, length ~19 mm `[measured, partly legible]`) with two thin flanges on opposite faces, each carrying a chevron bump. Female: rectangular cavity with two matching V recesses inside. Push in, flanges flex inward, bumps snap into the recesses; pull to release ("bi-directional") or set α′ = 90° and tighten for permanent. Flange dimensions follow the shared table (t 1.8→0.9, bump height = y 0.8, α 30°, α′ 45°). Print: tab part sits on the bed with the stem horizontal and flanges projecting sideways; chamfer the flange undersides ≤ 45° from vertical so no support is needed and the first layer is a plain square `[video]`.

### Forked detent pin (D5) `[video]`
Two prongs like a tuning fork press against the outer walls of a slot; small bumps on the prong tips drop into dimples in the slot and "pop". Prongs ≥ 0.9 mm thick (2 perimeters), ~10 mm tall, gap between prongs ≥ 2× bump height, bump 0.3–0.5 mm `[judgment]`, α = α′ ≈ 30–45° so it releases. Print with the fork profile in XY (the pin lying flat).

## Print
Profile in XY, extruded in Z. Overhanging hook faces ≤ 45°. 3+ perimeters; infill irrelevant for beams under 2.7 mm because they are all wall. PETG or ASA if the joint cycles often; PLA fine for a few cycles.

## Model it
1. Sketch the beam profile (root t, linear taper to t/2, hook with α and α′ faces) on the XY plane.
2. Extrude width b.
3. Fillet the root at 0.6·t.
4. Cut the mating slot/cavity with gap per the table; cut the undercut pocket y deep where the hook lands.
5. Chamfer the hook's downward face to 45° if it will print projecting sideways.

## Tune it
Too stiff or breaks: lengthen L or thin the tip (never below 0.9). Will not hold: deepen y, raise α′ toward 90°. Hard to insert: lower α to 20–25°, round the hook nose. Loose after a week in PLA: switch to PETG or halve ε.

## Failure modes
- Snaps at root: fillet missing, L/t under 8, or beam built in Z. Add fillet, lengthen, reorient.
- Hook shears off: undercut deeper than tip thickness allows; make tip ≥ 0.9 mm.
- Never latches: y smaller than gap + print error. Raise y to ≥ 0.6 + gap.
- Flange droops in print: underside steeper than 45°; chamfer it.
