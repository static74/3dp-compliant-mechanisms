# Spring-loaded detent plunger, Ø6 mm, 3 mm travel, PETG, metal pen spring

## Mechanism and why
**Question answered:** which spring and which retention method suit a Ø6 mm detent plunger with 3 mm of travel, held loaded, in PETG?

- **Spring: metal compression spring (your pen springs).** The skill's rule sends a spring that rests compressed (a preloaded detent) to metal, because printed plastic creeps. Travel above about 2 mm and "decent force" in a Ø6 envelope point the same way. A printed serpentine or leaf spring is the alternative, and it would only suit ≤ 2 mm travel with a light, unloaded rest. I did not use it.
- **Retention: Method A, one-way barbed plunger** (`spring-capture.md` A). The plunger's inner end is split into two prongs that carry local ears. You push the plunger in from outside, the ears snap behind the neck, and the 90° catch faces stop it coming out. I chose A over Method B (slicer pause) because the fixture body then prints on any machine with no mid-print stop. The plunger is a separate part that you can reprint on its own. A is not serviceable, so a lost plunger means a reprint.
- **Nose:** a printed hemispherical nose. No real ball is needed. A steel ball would need its own retainer.

## Parameters (Ø6 plunger, PETG, 0.4 mm nozzle, 0.2 mm layers)

Datums: the **catch step** is the inner face of the neck (Z = 0, positive outward). Travel s = 3 mm.

| Item | Value | Tag |
|---|---|---|
| Neck bore | Ø6.5 (0.25 per side), with a 4.24 mm chord flat, length Ln = 10.5, 0.5 × 45° mouth chamfer | `[source: Fictiv; judgment]`, flat `[derived]` |
| Catch step | square, 90°, never chamfered | `[source: Fictiv, BASF]` |
| Counterbore | Ø8.6 (ear span 7.6 + 0.5, rounded up for printed-hole allowance) | `[source: Bayer; judgment]` |
| Ear axial length a | 1.7 (30° lead-in over 0.8 ≈ 1.4, plus 0.3 land) | `[derived]` |
| Cavity depth, catch step to floor | a + Li = 1.7 + 14 = 15.7 | `[derived]` |
| Plunger body | Ø6 with 4.24 mm flat (0.88 deep), Lb = 1.0 | `[derived]` |
| Split zone | Ø6 (no turn-down), Ls = 12.5, slot 1.9, prongs 2.05 thick, L/h = 6.1 | `[judgment]` |
| Root fillet at slot end | 1.05 (0.5·h) | `[source: Hubs, Bayer]` |
| Ears | on the two outer prong faces only, never a ring. Span Ø7.6, 2 mm tall (\|z\| ≤ 1), 30° lead-in, 90° catch face, 45° chamfer on the z-faces | `[derived]` |
| Squeeze per prong | 0.6 mm to clear the round neck at the ear edges | `[derived]` |
| Prong strain | ε = 1.5·0.6·2.05/12.5² = 1.2 % vs 3.6 % PETG one-time | `[derived from Bayer]` |
| Catch overlap | 0.55 at z = 0, 0.58 at z = 1 (≥ 0.5) | `[judgment]` |
| Slot check | needs ≥ 2×0.6 + 0.3 = 1.5, so 1.9 closes with margin | `[derived]` |
| Outer shoulder | Ø8 × 2 mm, bottom face 3 mm proud of the housing face at rest | `[derived]` |
| Nose | Ø3 cylinder, hemispherical tip (R1.5), 2.5 mm long beyond the shoulder | `[judgment]` |
| Detent pocket (knob) | 1.5 mm deep, width = nose + 0.6 = 3.6, 30–45° ramps | `[judgment]` |

Stack checks:
- Ls + Lb = 12.5 + 1.0 = 13.5 = Ln + s = 10.5 + 3. This puts the shoulder 3 mm proud at rest and flush with the housing face at full travel.
- Neck guidance: at rest the neck holds plunger 0…10.5, which is all split zone. At full travel it holds 3…13.5 (split zone 3…12.5 plus the 1 mm body). The plunger always has full-diameter guidance.
- Counterbore Ø8.6 exceeds the ear span of 7.6, so the prongs relax fully and never rub.
- The ears bear on the catch step with 0.55 mm overlap, which exceeds the 0.5 mm minimum.

## Your pen springs: measure, then pick one
Pen springs are long and soft, about 0.2–0.5 N/mm `[judgment]`. At 3 mm that is thin on force, so select and modify the spring as follows.

1. Measure OD, wire diameter, free length, and solid height. Press it 5 mm on a kitchen scale for the rate k. Pick one with OD ≤ about 5.4 mm. The 5.4 figure matches the worked cavity above. Larger OD needs a larger counterbore: use max(7.6, OD) + 0.5, rounded up.
2. Raise the rate by cutting coils: k ∝ 1/n. Keep free length / mean diameter ≤ 4. Mean diameter is about 5, so free length ≤ about 20. Bend or grind the cut end flat. Close up the last coil so the wire end cannot poke into the 1.9 mm slot. Mean diameter ≈ 4.95 sits between the slot and Ø6, so the end coil bears on both prong tips.
3. Treat a cut spring as unqualified. Compress it to working length ten times, and reject it if the free length drops more than 2 %. Keep service compression ≤ 60 % of (free − solid).
4. Set the geometry from the spring you keep. Preload = 15–25 % of (free − solid), so Li = free − preload. Cavity depth = 1.7 + Li. Check Li − 3 ≥ solid + 1.

Example from the worked case: 16 mm free spring, 2 mm preload, Li = 14. This needs solid ≤ 10.

Force with that spring:
| k (N/mm) | At rest (2 mm preload) | Riding the 1.5 mm ramp | At full 3 mm stop |
|---|---|---|---|
| 0.3 | 0.6 N | 1.1 N | 1.5 N |
| 0.5 | 1.0 N | 1.75 N | 2.5 N |

If your best cut pen spring gives less than you want, use a stock part rather than stacking pen springs. Nesting two springs, or buying stock, is the skill's guidance above about 3–4 N at 3 mm travel. Lee LC 026C 05 S (rate 1.82 N/mm, OD 6.1) is the nearest stock Ø6 option, and it needs a counterbore of about Ø8.6 or more. Its part number is from the skill's list. Check it against the actual part you buy.

Detent holding force ≈ spring force × tan(ramp angle) plus friction (μ ≈ 0.4–0.5 PETG on PETG, unsourced) `[judgment]`. Steeper ramps hold harder, and 45° holds harder than 30°. The pocket is 1.5 mm deep, which is half the travel. The other 1.5 mm is over-travel margin before the shoulder hits the housing. Only the first 1.5 mm is working stroke.

## How it cannot fall out
- The ears have a 90° catch face against the catch step. Only shearing the ears removes the plunger.
- Retention check: the spring pushes with 1–2.5 N, which is far below the shear strength of 2 mm tall by about 1 mm deep PETG ears `[judgment]`.
- The outer shoulder stops over-insertion, so the plunger cannot be pushed through the housing.
- The flat in the bore stops rotation, so the ears always sit over the catch.

## Print orientation
- **Plunger: on its side**, slot plane perpendicular to the bed, flat on the bed. The prongs sit left and right of the slot and flex within each layer. Upright, each prong is a cantilever across layer lines and snaps `[video]`.
- Bed footprint: the slot splits the flat, leaving (4.24 − 1.9)/2 = 1.17 mm of bed contact per prong. **Do not put the 0.4–0.6 mm first-layer chamfer on the prong flats** (fundamentals §8 exempts footprints under 3 mm). Chamfer only the body ends. The ears' lowest point is 1.12 mm above the bed plane, and their 45° z-face chamfer needs no support.
- Keep the perimeter seam off the prongs. Check the sliced toolpath: the 2.05 mm prongs should be 4–5 perimeters, and the 1.9 mm slot should survive.
- **Housing: print with the bore horizontal**, using teardrop sections for the neck and counterbore. The catch step is a downward annular overhang with 1.05 mm radial depth, slightly over the 1 mm rule, so do not print it bore-up with a flat ceiling. Put the bore flat at the bed side, and do not chamfer the catch step.
- Set elephant-foot compensation ≈ 0.2 mm. Round vertical corners R ≥ 2 mm.

## CAD steps
1. Housing: bore the Ø6.5 neck, 10.5 long, with the 4.24 mm flat, then the Ø8.6 counterbore behind it. Make the catch step square. Set cavity depth from the catch step to the floor to 1.7 + Li. Add the 0.5 × 45° mouth chamfer.
2. Plunger, drawn outside in: R1.5 nose, Ø8 × 2 shoulder, Ø6 body with flat (1.0 long), then the 12.5 mm split zone with the 1.9 slot and R1.05 root fillet.
3. Add the two ears (Ø7.6 span, |z| ≤ 1, 30° lead-in, 90° catch face, 45° z-face chamfers).
4. Cut the 1.5 mm deep pocket in the knob rim, 3.6 wide, with 30–45° ramps. Place the race surface so the nose tip protrudes 1.5 mm beyond it at rest. Check that clearance holds with the shoulder 3 mm proud of the housing face.
5. Assembly: drop the spring in the counterbore, then push the plunger in from the mouth until the ears click behind the catch step.

## Tune it
One test print is needed before you rely on any `[judgment]` value. These are the bore clearances, the 0.55 mm catch overlap, the pocket depth, ramp angles, spring cut, and prong behaviour.
- Print a short test housing with the neck and a few cavity lengths, and the plunger only.
- The plunger sticks: raise bore clearance to 0.3 per side, check the flat, and look for ooze blobs in the bore.
- The ears do not pass the neck, or a prong cracks: confirm the plunger printed on its side, then check the squeeze against the actual printed neck diameter.
- The plunger pops out: the catch face was chamfered or the overlap was too small. Reprint with 0.2 mm more ear height.
- The click is too weak: shorten the spring by cutting coils, add preload, or use a stiffer stock spring.
- The click is too hard: use shallower ramps, 30° instead of 45°.
- The spring buckles or rubs: free length / mean diameter is above 4. Shorten it.

## Flagged `[judgment]` values, each needing one test print
Nose radius and length, pocket depth and width, ramp angles, catch overlap, prong thickness and length, neck and counterbore allowances, and the pen-spring rate and cut. Strains are derived from moulded-plastic rules, not measured on printed beams.
