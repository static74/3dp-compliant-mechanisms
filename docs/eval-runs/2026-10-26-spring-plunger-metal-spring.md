# Spring-loaded detent plunger, 6 mm, 3 mm travel, PETG, Prusa Core One

Tags follow the skill: `[video]`, `[measured]`, `[source]`, `[derived]`, `[judgment]`. Every `[judgment]` value needs one test print (listed at the end).

## 1. Mechanism and why

**Question answered:** which spring and which capture method suit a 6 mm plunger with 3 mm travel, decent force, a bag of pen springs, and a hard requirement that the plunger cannot fall out?

- **Spring: metal compression spring (pen spring), not a printed spring.** Travel of 3 mm exceeds the ~2 mm printed-leaf limit, the spring rests preloaded (PETG creeps under constant load), and the force target is above what a printed leaf gives in this envelope (spring-loaded.md decision table). The printed alternative (serpentine or cantilever leaf, ≤ 2 mm travel, light force) is offered but does not meet your numbers.
- **Capture: method A, the one-way barbed plunger** (spring-capture.md A). Reasons: you want a separate plunger you can print and swap, you have no need for a slicer pause, and the barbs make "cannot fall out" mechanical rather than dependent on assembly. Method B (pause and seal the spring in) would lock the spring but still leave the plunger to be retained by some other feature, and it needs a 9 mm-wide enclosed cavity bridge.
- **Nose:** a ramped, rounded nose that rides in V-shaped pockets on the knob. Symmetric ramps suit a knob that turns both ways. A real steel ball is not needed; a printed rounded nose is the "ball-detent style" here.
- **Pen springs:** they are long and soft. Cutting one shorter removes active coils and raises its rate (rate scales as 1/active coils), so you can tune force without buying parts. Section 3 shows how to choose one.

## 2. Parameters

Plunger body Ø6.0, one-time-snap barbs, PETG, 0.4 mm nozzle, 0.2 mm layers. Axial positions run from the housing's outer face inward.

| Feature | Value | Tag |
|---|---|---|
| Plunger body diameter | 6.0 mm (your spec) | given |
| Neck bore (outer face, guides the plunger) | Ø6.5 (0.25 per side) | `[source: Fictiv]` + `[judgment]` allowance |
| Neck length | 5.0 mm (about 0.8 d guide length) | `[judgment]` |
| Anti-rotation flat | 0.9 mm deep on the plunger (chord 4.2 mm); matching flat on the bore floor at 2.35 mm from the axis (0.25 clearance) | flat depth `[derived]`: puts the flat edge at 45° so no support is needed; fit `[judgment]` |
| Split zone | 2 prongs, length L = 10 mm | `[judgment]` (8-12) |
| Slot between prongs | 2.4 mm at the root, widening to 3.6 mm at the tips (prongs taper 1.8 to 1.2 mm thick). Minimum slot is 2y + 0.3 = 2.3 mm | `[derived]` |
| Prong root fillet | 0.9 mm | `[source: Hubs, Bayer]` (≥ 0.5 h) |
| Barb height y | 1.0 mm per side, so barb outer Ø8.0 | `[judgment]`; limit `[derived]` y ≤ ~2.0 mm (PETG one-time, L 10) |
| Barb lead-in | 30° from axis, 1.8 mm long | `[source: Bayer]` |
| Barb catch face | 90°, never chamfered; 0.4 mm flat land after the lead-in | `[source: Fictiv, BASF]`, land `[judgment]` |
| Catch overlap | 1.0 mm barb height minus 0.25 mm radial clearance = 0.75 mm (≥ 0.5) | `[derived]` |
| Prong strain on insertion | deflection 0.75 mm, ε ≈ 0.75·1.8/(1.09·10²) = 1.2 %, below the 3.6 % one-time PETG limit | `[derived]` Bayer taper formula, fundamentals §4 |
| Counterbore (behind the neck) | Ø9.0 (neck radius 3.25 + y 1.0 + 0.25 = 4.5 radius) | `[source: Bayer stress-free rule; margin judgment]` |
| Counterbore depth C | C = installed spring length + 2.2 mm (barb length). Example below: 12.2 mm | `[derived]` |
| Spring seat | flat shoulder across both prong tips, from radius 1.8 to 4.0 mm, so the end coil bears on both prongs | `[source: spring-loaded.md Model it]` |
| Detent nose | rounded tip R1.5 mm, protrudes 1.5 mm into the knob pocket | `[judgment]` |
| Nose ramps | 30° from the knob surface, both sides (soft click). Use 45° for a firmer hold | `[source: Bayer]` 30°/45° |
| Knob pocket | V or round pocket, 1.5 mm deep, matching ramps, corners rounded | `[source: spring-loaded.md]` (1.0-1.5 mm) |
| Travel | 3.0 mm total. 1.5 mm is used by ride-over; the other 1.5 mm is margin | `[judgment]` |
| Outer shoulder | Ø8 flange, 1.5 mm thick, stops over-insertion at the housing face | `[source: spring-loaded.md]` |

Why the housing has two bores: the Ø6.5 neck guides the plunger and holds the catch; the Ø9 counterbore only gives the barbs room to spring open. The step between them is the catch ring the barbs hook on. The spring sits inside the counterbore.

## 3. Choosing and sizing the pen spring

Measure each candidate with calipers: outer diameter, wire diameter, free length, solid height. Press it on a kitchen scale to 5 mm compression and divide the reading in newtons by 5 to get the rate in N/mm.

Selection rules (spring-loaded.md B):

1. Outer diameter ≤ 6.0 mm (it must fit the Ø6.5 bore with ≥ 0.35 mm diametral room, and it grows when compressed).
2. Free length / mean diameter ≤ 4 after cutting, so no guide pin is needed (Norton rule, `[source]`). This is why a cut spring suits the Ø9 counterbore.
3. Install with 15-25 % of full deflection as preload; never go beyond 85 % of full deflection in service `[judgment]`.

Worked example with assumed pen-spring numbers (replace with your measurements): wire 0.45 mm, mean diameter 5.15 mm, steel G ≈ 79 GPa. Rate k = G·d⁴/(8·D³·Na) ≈ 3.0/Na N/mm. Cut to 5 active coils: k ≈ 0.6 N/mm, free length 12 mm, solid about 3.5 mm, so full deflection is about 8.5 mm. Install at 10 mm (2 mm preload, 24 % of full). Force when extended is 1.2 N. At 3 mm travel the spring is at 7 mm (5 mm compressed, 59 % of full, force 3.0 N). That sits inside the 85 % limit with 3.5 mm to spare before solid. `[derived]`

Then C = 10 + 2.2 = 12.2 mm counterbore depth.

How much force is "decent"? Pen springs top out near 3-4 N at this travel. If that is not enough: (a) nest two pen springs, one inside the other, wound opposite hands, which adds their rates; (b) buy a stock spring from spring-loaded.md, for example LC 026C 05 S (OD 6.10, 1.82 N/mm) or LC 022B 05 S (OD 4.57, 2.05 N/mm); the 6.10 OD part needs the bore enlarged to about 6.7 mm. Tell me the measured numbers and I will fix the housing depth and bores.

Rotary effect: a knob torque is tangential force times pocket radius. With friction μ = 0.5 (PETG on PETG, `[judgment]`) and a 30° ramp, the tangential force is about 1.5 times the spring force (W = P(μ + tan α)/(1 − μ tan α), `[source: Bayer]`). A 45° ramp raises the factor to 3. A smear of PTFE grease or PTFE tape on the nose and bore cuts μ to about 0.2 and the factor to about 0.9 `[judgment]`.

## 4. Print orientation

**Plunger:** lie it on its side with the 0.9 mm flat on the bed and the slot plane vertical (perpendicular to the bed). The prongs then sit left and right of the slot and flex within each layer, along the deposited lines. Printed upright, each prong is a Z cantilever and snaps along a layer line `[video]`. Settings: 0.2 mm layers, 3-4 perimeters, 100 % infill, no supports, elephant-foot compensation about 0.2 mm, 0.4 mm 45° chamfer on the bed edge of the shoulder `[source: fundamentals §8]`. Keep the seam away from the prong roots. Use a short 0.3 mm sacrificial tie or mouse ear if the thin prong tips lift.

**Housing:** print it with the bore axis horizontal. Model both the Ø6.5 neck and the Ø9 counterbore as teardrops with 45° flats, apex truncated to a flat ≤ 3 mm `[source: fundamentals §9]`. Bore-up would give a 1.25 mm annular overhang at the catch step (above the 1 mm limit, and the step must stay 90°). Bore-down would put a 9 mm bridge over the spring cavity floor. Horizontal avoids both. Do not chamfer the catch step on the housing or the plunger.

## 5. CAD steps

1. Housing: sketch the neck as Ø6.5 with the floor flat at 2.35 mm below the axis; extrude 5.0 mm in from the outer face.
2. Cut the Ø9.0 counterbore, depth C (12.2 mm in the example), flat-bottomed, leaving at least 2 mm of wall behind it. Convert both bores to teardrops (step 4 of orientation).
3. Plunger: revolve Ø6.0 body to the required length, add the Ø8 outer shoulder, and cut the 0.9 mm flat along one side for the full length.
4. Split zone: cut the tapered slot (2.4 to 3.6 mm wide) through the inner 10 mm, with the slot plane perpendicular to the flat. Fillet prong roots at 0.9 mm.
5. Add barbs on the outside of each prong tip: 1.0 mm tall, 30° lead-in over 1.8 mm, 0.4 mm land, then a 90° catch face. Make the tip face a flat spring seat.
6. Detent nose: R1.5 rounded tip with 30° ramps, 1.5 mm protrusion.
7. Knob: cut 1.5 mm deep matching pockets at each detent position, edges rounded.
8. Check: with the plunger fully out, the catch face touches the neck step; fully in (3 mm), the barb tips are 0.5 mm clear of the counterbore wall and the spring is still ≥ 3 mm from solid.
9. Assembly: drop the spring into the counterbore (via the neck), then push the plunger in by hand from outside. The barbs snap behind the step. Nothing short of shearing the barbs removes it, and the spring force (about 3 N) is far below the barb shear strength `[judgment]`.

## 6. Tuning note

- Weak or soft click: cut the spring one coil shorter (rate rises), or add preload by shortening C by 0.5 mm.
- Plunger sticks: widen the neck clearance to 0.30 per side, check for ooze blobs in the bore, add PTFE grease.
- Rattles: add preload up to the 25 % guide.
- Barbs scrape the counterbore: the barbs are too tall for the wall; keep the 0.25 mm margin.
- Do not tune the slicer to make anything fit. If a fit is wrong, the geometry above is wrong, not the printer.

## 7. Test print before the real part

Print one 20 mm-long housing cross-section (neck + counterbore only, 2 mm walls) and one plunger. Check these `[judgment]` values: neck clearance and flat clearance, barb height 1.0 mm (the barbs must pass the neck by hand and hold against a firm pull), spring seat fit with your actual pen spring, and the feel of the 30° nose ramps against a pocket test piece. Adjust one value at a time.
