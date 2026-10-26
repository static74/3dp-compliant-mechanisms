# Spring-loaded mechanisms: plungers, buttons, detents, latches

**Family:** spring-loaded (a moving plunger, latch or shoe pushed by a spring)
**Use when:** a feature must move 1–10 mm and return: latch lids, push buttons, ball/pin detents, pogo-style contacts, spring-loaded doors.
**Avoid when:** a passive flexure (grip fins, side spring, snap-fit) already gives enough travel; those are simpler and have no loose parts.
**Source:** Slant 3D springs and snap videos; Akaki Kuumeri flexure talk; Bayer; Lee Spring catalog. Research tables in `docs/research/lids-and-spring-parameters.md` topics B–C.

## Decision: printed spring or metal spring
| Condition | Choose | Why |
|---|---|---|
| Travel ≤ ~2 mm, spring rests unloaded or lightly loaded, few hundred cycles | **Printed** serpentine or cantilever leaf | one part, no assembly, Slant's latch class `[video]` |
| Spring rests compressed (preloaded detent, plunger held in) | **Metal** | printed plastic creeps; PLA loses force in days `[source: Kuumeri]` |
| Travel > 3 mm or force > ~5 N in a small envelope | **Metal** | a printed beam long enough would not fit |
| Must be a helical compression spring | **Metal** | Slant: "the one spring we will never make is a coil spring" `[video]`; printed coils only work lying on their side `[source: He 2022]` |
Always state the choice and offer the other. A metal spring requires one of the two capture methods in `spring-capture.md`.

## A. Printed springs `[video + source: Kuumeri]`
Master rule: all spring force lies in the layer plane. Print the spring flat with its bending profile in XY; "if you try to print this spring at an angle you just ruined the spring" `[video]`.
| Geometry | Works? | Notes |
|---|---|---|
| Serpentine / zigzag flat spring | yes | beams ≥ 0.86 mm (2 perimeters), down to 1 mm for soft; round every bend, square bends break just below the curve `[video]` |
| Cantilever leaf (side-turned snap arm) | yes | the latch class; see sizing below |
| Ring / trampoline leaf, spiral (clock) spring | yes | thicken in Z for stiffness without raising strain `[video]` |
| Helical coil | no (printed vertical) / fallback lying on its side | wire ≥ 1.6 mm, Ø ≥ 4 mm `[source: He 2022]` |
| Wave spring | no | crests load across layers `[judgment]` |

### Sizing a printed leaf for a latch
| Parameter | Value | Tag |
|---|---|---|
| Beam thickness t | 0.86 mm (2 perimeters at 0.2 mm layers) or 1.2–1.3 mm for a 0.6 mm nozzle; never 3+ lines of gap-filled wall | `[source: Prusa KB, Kuumeri]` |
| Beam depth (in Z) | ≥ 10 mm; narrower twists | `[source: Kuumeri]` |
| Length for 2 mm travel at t 0.86 | PLA one-time 11.4 mm; PLA repeated 14.7 mm; PETG repeated 11.1 mm; held for days 27 mm | `[derived, L = √(1.5·t·y/ε)]` |
| L/t | ≥ 10 for the formula; ≥ 25 for long-life springs | `[source: BASF, Kuumeri]` |
| Strain | PLA 1.2 %, PETG 2.1 % repeated; ≤ 0.35–0.5 % if held | fundamentals §4 |
| Hard stops | always, so the user cannot overbend | `[source: Kuumeri]` |
| Seam | keep the perimeter seam off the flexure; filleted corners attract it | `[source: Kuumeri]` |
| First layer of thin tips | tie to the body with a ~0.3 mm sacrificial connector or mouse ears | `[video]` |
| Overhang above a spring | 45° chamfer, never a flat bridge, so it cannot sag onto the spring | `[video]` |
Material: PETG default (yield 5.1 % vs PLA 2.9 %, HDT 68 vs 55 °C). PLA for short-lived or rarely flexed parts only `[source: Prusament TDS]`.
Embedded springs: a flat spring can be printed fully enclosed inside the part if its bending plane is the layer plane `[video]`.

## B. Metal compression spring `[source: Lee Spring, Norton]`
Pick from stock; do not design a custom spring. Verified stainless parts (Lee LC series, squared and ground):
| Part | OD | Wire | Free L | Rate N/mm | Solid | Lee hole |
|---|---|---|---|---|---|---|
| LC 014A 05 S | 3.05 | 0.36 | 12.70 | 0.75 | 3.96 | 3.18 |
| LC 016A 09 S | 3.05 | 0.41 | 19.05 | 0.74 | 7.75 | 3.18 |
| LC 018B 05 S | 4.57 | 0.46 | 12.70 | 1.02 | 3.35 | 4.78 |
| LC 022B 05 S | 4.57 | 0.56 | 12.70 | 2.05 | 4.78 | 4.78 |
| LC 018B 09 S | 4.57 | 0.46 | 19.05 | 0.58 | 5.05 | 4.78 |
| LC 026BC 08 S | 5.33 | 0.66 | 20.65 | 1.45 | 8.74 | 5.56 |
| LC 020C 05 S | 6.10 | 0.51 | 12.70 | 0.72 | 3.35 | 6.35 |
| LC 026C 05 S | 6.10 | 0.66 | 15.88 | 1.82 | 5.16 | 6.35 |
| LC 020C 09 S | 6.10 | 0.51 | 19.05 | 0.47 | 4.62 | 6.35 |
| LC 022D 03 S | 7.62 | 0.56 | 15.88 | 0.74 | 3.10 | 7.95 |
Any equivalent (pen springs, McMaster 9657K series, assortment kits) works if you measure OD, free length and solid height; those part numbers were not verified.

Design rules:
| Rule | Value | Tag |
|---|---|---|
| Printed bore diameter | Lee hole + 0.2–0.3 mm ≈ spring OD + 0.35–0.6 mm diametral; print a test bore | `[source: Lee; allowance judgment]` |
| OD grows when compressed | check OD at installed length against the bore | `[source: Lee]` |
| Buckling | free length / mean diameter ≤ 4 with both ends seated needs no guide; above 4, or one end free to tip, run it in a bore or over a pin | `[source: Norton]` |
| Guide pin | ≤ Lee rod diameter − 0.2 mm | `[judgment]` |
| Preload at installed length | 15–25 % of full deflection (free − solid) so nothing rattles; never past 85 % in service | `[judgment, consistent with Shigley band]` |
| Example | LC 018B 05 S: full deflection 9.35 mm; install at 11.0 mm (1.7 mm, ≈1.7 N); keep ≥ 1.4 mm from solid | `[derived]` |
| Max force check | rate × max compression must stay well below the force to shear the retaining barbs | `[judgment]` |

## Plunger body (either spring)
Sliding clearance 0.2–0.3 mm per side to the bore `[source: Fictiv; judgment]`. Add a flat on the plunger and bore so it cannot rotate and so the plunger prints on its side `[judgment]`. Detent nose: 30° insertion ramp, 45° release ramp (or 90° to hold) `[source: Bayer]`. Give the plunger an outer shoulder larger than the neck so it cannot be pushed in too far; the retention feature (barbs or sealed roof) stops it coming out.

## Model it (metal spring, barbed plunger)
1. Housing: bore = spring OD + 0.5 mm diametral, depth = installed spring length + plunger travel + barb length; neck at the outer face = plunger body + 0.5 mm diametral; counterbore behind the neck per `spring-capture.md` A.
2. Plunger: detent tip, sliding body, split zone with two prongs and barbs at the inner end (see `spring-capture.md` A for all barb numbers), flat along one side.
3. Mating detent pocket in the other part, 1.0–1.5 mm deep with matching ramps.
4. Spring seat: a flat shoulder at the prong tips so the end coil bears on both prongs and cannot enter the slot.

## Tune it
Weak return: stiffer spring (next wire size) or more preload. Sticks: increase bore clearance to 0.3/side, add the flat, check for ooze blobs in the bore. Printed leaf relaxes: PETG, lengthen L, or go metal.

## Failure modes
- Printed spring snaps: built at an angle or square bends; print flat, round bends.
- Plunger ejected by spring: capture failed; see spring-capture.md.
- Spring buckles and rubs: Lf/Dm > 4 without a guide.
- Roof sags onto the moving part: use a 45° chamfered roof or the pause-and-cap method.
