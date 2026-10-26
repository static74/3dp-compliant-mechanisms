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
Any equivalent (pen springs, McMaster 9657K series, assortment kits) works if you measure it; those part numbers were not verified.

### Using an unknown or pen spring `[judgment; formula is textbook]`
Measure OD, wire diameter d, free length, solid height, and count active coils n. Rate k = G·d⁴ / (8·D³·n) with D = OD − d (mean diameter) and G ≈ 79 GPa for steel wire; or press it 5 mm on a kitchen scale and divide. Pen springs are long and soft (≈ 0.2–0.5 N/mm). Cut to fewer active coils to raise the rate (k ∝ 1/n) and bring free length / D under 4; grind or bend the cut end flat so it seats. A cut spring is an unqualified spring: re-measure rate, free length and solid height, compress it to the working length ten times and reject it if the free length drops more than 2 % (permanent set), and keep service compression ≤ 60 % of (free − solid) because its wire stress is unknown `[source: Lee white paper for the set check; limits judgment]`. Nest two springs or buy stock for more than ≈ 3–4 N at 3 mm travel.

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

## Detent nose geometry
Linear or one-way latch: 30° insertion ramp, 45° release ramp (90° to hold) `[source: Bayer]`. Rotary or ball detent that must click both ways: symmetric 30–45° ramps or a hemispherical nose of radius ≈ plunger radius/2, pocket depth ≈ half the travel with the rest as margin, pocket width = nose width + 0.6 mm `[judgment]`. Detent force ≈ spring force × tan(ramp angle) plus friction (μ ≈ 0.4–0.5 PETG on PETG, unsourced).

## Plunger body (either spring)
Sliding clearance 0.2–0.3 mm per side to the neck bore `[source: Fictiv; judgment]`. Add a flat on the plunger and a matching flat in the bore so it cannot rotate and so it prints on its side: for the bed edge to stay at or under 45° the flat chord must be ≥ 0.71·D (D/√2), which is a flat 0.15·D deep (Ø6: chord 4.24 mm, depth 0.88 mm) `[derived]`. Give the plunger an outer shoulder larger than the neck so it cannot be pushed in too far; the retention feature (barbs or sealed roof) stops it coming out.

## Axial datums (use these names in every dimension)
- **Neck bore**: the narrow hole at the housing's outer face that the plunger body slides in. Ø = D + 0.4–0.6 mm.
- **Catch step**: the inner face of the neck, where the barbs' 90° faces land. Z = 0 for every depth below.
- **Counterbore**: the wider cavity behind the catch step holding barbs and spring. Ø ≥ max(spring OD + 0.5, barb span + 0.5); it is never smaller than the deployed barb span in any branch.
- **Spring seat**: the shoulder at the prong tips that the spring's end coil bears on, at depth `a` = barb length from the catch step when the plunger rests against the catch.
- **Cavity depth** (catch step to floor) = `a` + installed spring length Li. Travel comes from compressing the spring, not from extra cavity length.
- **Outer shoulder**: on the plunger outside the housing, sets maximum inward travel s. Check Li − s ≥ solid height + 1 mm so the spring never goes solid, and the barbs never need to reach the floor.
- **Preload** = free length − Li, set at 15–25 % of (free − solid) `[judgment]`.

## Model it (metal spring, barbed plunger, worked for D = 6 mm PETG)
Axial layout, origin at the catch step, positive outward. Neck occupies 0…Ln. At rest the barb catch faces sit at 0 (inside the counterbore), the split zone runs 0…Ls, the body Ls…Ls+Lb, and the outer shoulder at Ls+Lb must sit s (travel) beyond the housing face: **Ls + Lb = Ln + s**. The neck guides whatever part of the plunger is inside it, so the split zone stays at full body diameter.
Cross-section conventions: x is the flex direction (left/right of the slot), z is along the slot plane, the bed plane is at z = −2.12 (the 4.24 mm flat).
1. Housing: neck bore Ø6.5 with the 4.24 mm flat, Ln = 10.5 mm, mouth chamfer 0.5 × 45°; catch step square; counterbore Ø8.6 (ear span 7.6 + 0.5 = 8.1 governs over spring OD 5.4 + 0.5; rounded up for the printed-hole allowance); cavity depth from the catch step = a + Li, with a = ear axial length (30° lead-in over 0.8 mm ≈ 1.4 mm plus a 0.3 mm land ≈ 1.7 mm) and Li = installed spring length, e.g. 1.7 + 14 = 15.7 mm for a 16 mm free spring at 2 mm preload.
2. Plunger, outside in: detent nose; outer shoulder Ø8 × 2 mm; body Ø6 with the flat, Lb = Ln + s − Ls = 10.5 + 3 − 12.5 = 1.0 mm; split zone Ø6 (no turn-down), Ls = 12.5 mm, slot 1.9 mm, prongs (6 − 1.9)/2 = 2.05 mm thick (4–5 perimeters), L/h = 6.1; root fillet 1.05 mm (0.5·h) at the slot end.
3. Barbs are **local ears on the two outer prong faces, not a ring**: a ring segment beside the slot would stand 3.68 mm from the axis in z and could never pass the 3.25 mm neck radius however far the prongs squeeze. Each ear: outer face on the Ø7.6 cylinder (y = 0.8 above the body), confined to |z| ≤ 1.0 (2 mm tall), 30° lead-in on the axial end, square 90° catch face, and a 45° chamfer on its z-faces so its underside is not a flat overhang. Squeeze needed so the whole ear clears the round neck: at z = 1 the ear surface sits at x = 3.67 and must reach x ≤ √(3.25² − 1²) = 3.09, so squeeze = 0.6 mm per prong (0.55 at z = 0). ε = 1.5·0.6·2.05/12.5² = 1.2 % against PETG one-time 3.6 % and PLA 2.0 % `[derived]`. Catch overlap = 0.55 at z = 0 and 0.58 at z = 1, both ≥ 0.5. Slot ≥ 2 × 0.6 + 0.3 = 1.5, so 1.9 closes with margin.
4. Stroke check: at rest the neck holds plunger 0…10.5 (split zone); at full travel it holds 3…13.5 (split zone 3…12.5 plus the 1 mm body). Spring: Li − s = 14 − 3 = 11 ≥ solid 6 + 1 `[derived]`.
5. Footprint on its side: one bed plane at z = −2.12 along the whole plunger; the slot splits the flat over the split zone, leaving (4.24 − 1.9)/2 = 1.17 mm of bed contact per prong. **Do not apply the blanket bed-edge chamfer to the prong flats** (fundamentals §8 exempts footprints under 3 mm); chamfer only the body ends. The ears sit at |z| ≤ 1, so their lowest point is 1.12 mm above the bed plane with the 45° ear chamfer below it `[derived]`.
6. Mating detent pocket in the other part, 1.0–1.5 mm deep with ramps matching the nose.
7. Assembly: spring into the counterbore first (mean diameter 4.95 mm sits between the 1.9 mm slot and the Ø6 prong tips so the end coil bears on both prongs), then push the plunger in until the ears click.

## Tune it
Weak return: stiffer spring (next wire size) or more preload. Sticks: increase bore clearance to 0.3/side, add the flat, check for ooze blobs in the bore. Printed leaf relaxes: PETG, lengthen L, or go metal.

## Failure modes
- Printed spring snaps: built at an angle or square bends; print flat, round bends.
- Plunger ejected by spring: capture failed; see spring-capture.md.
- Spring buckles and rubs: Lf/Dm > 4 without a guide.
- Roof sags onto the moving part: use a 45° chamfered roof or the pause-and-cap method.
