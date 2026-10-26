# Spring-loaded detent plunger, 6 mm, 3 mm travel, PETG

## Mechanism and why

**Question answered:** which spring, and how do we keep the plunger from falling out?

- **Spring: metal compression spring (your pen springs), with a printed leaf as the alternative you could try.** A printed leaf spring works only to about 2 mm of travel and does not like resting compressed, because printed plastic creeps while preloaded `[source: Kuumeri, spring-loaded.md]`. Your fixture needs 3 mm of travel and a detent that sits preloaded, so metal is the correct choice. A printed serpentine or cantilever leaf (PETG, beams 0.86 mm, 2 perimeters, printed flat) is still a valid fallback if you want one-piece and can live with about 2 mm travel and less force.
- **Capture: Method A, a one-way barbed plunger.** Two prongs on the plunger's inner end carry barbs with a 30 degree lead-in and a 90 degree catch face. You push the plunger in from outside, the barbs squeeze through the neck and spring open in the counterbore, and the 90 degree faces then lock behind the neck. Nothing short of shearing the barbs pulls it out, so it cannot fall out. I chose A over Method B (slicer pause with the spring sealed in) because the parts print separately, you assemble by hand, and no pause marker has to be placed correctly on a Prusa Core One.
- **Detent style:** a hemispherical nose that clicks both ways into pockets in the knob. Use symmetric 30 to 45 degree ramps `[source: Bayer; judgment]`.

## Step 0: characterise the pen springs (do this first)

Pen springs vary, so select by measurement `[judgment; formula is textbook]`.

1. Measure OD, wire diameter d, free length, solid height, and count active coils n.
2. Rate k = G·d⁴ / (8·D³·n), with D = OD minus d and G about 79 GPa for steel. Or press the spring 5 mm on a kitchen scale and divide the force by 5.
3. Pen springs are long and soft, about 0.2 to 0.5 N/mm. You asked for "decent force", so pick the stiffest wire in the bag (about 0.5 mm or thicker), then raise the rate by trimming coils (k scales as 1/n). Keep free length divided by D at or below 4 so it does not buckle, and grind the cut end flat so it seats. For more than about 3 to 4 N at 3 mm travel, nest two springs of opposite hand or buy stock (for example Lee LC 026C 05 S, 6.1 mm OD, 1.82 N/mm) `[judgment; part number from spring-loaded.md]`.
4. Accept a spring with OD about 4.5 to 6.5 mm. The mean diameter must sit between the slot width (1.9 mm) and the plunger diameter (6 mm) so the end coil bears on both prong tips.

Worked example, assumed spring: OD 5.4, d 0.45, trimmed to 16 mm free, k about 0.5 N/mm, solid about 6 mm. Full deflection is 10 mm. Install at 14 mm (2 mm preload, about 1 N at rest, 20 % of full deflection; the target is 15 to 25 %). At full 3 mm travel the spring is at 5 mm compression, or 50 % of full deflection, about 2.5 N, well under the 85 % limit `[derived, rule from judgment]`. Detent force is roughly spring force times tan(ramp angle) plus friction (mu about 0.4 to 0.5 for PETG on PETG, unsourced), so a 30 degree ramp gives about 0.6 to 1.5 N of click. If that feels weak, use a stiffer or nested spring, or steepen the ramps toward 45 degrees. Recompute every length below with your real Li (installed spring length).

## Parameters

| Feature | Value | Tag |
|---|---|---|
| Plunger body diameter | 6.0 mm, with a flat (see orientation) | given |
| Neck bore diameter | 6.5 mm (0.25 mm per side sliding clearance, range 0.2 to 0.3) | `[source: Fictiv; judgment]` |
| Neck length | about 10 mm (guides the plunger and holds the prongs) | `[judgment]` |
| Prong length L | 9 mm (range 8 to 12; L/h at least 6) | `[judgment]` |
| Prong thickness h | tapered 1.8 mm at root to 1.2 mm at barb (2 to 3 perimeters) | `[judgment; taper source: Bayer]` |
| Slot between prongs | 1.9 mm (2 x barb height + 0.3) | `[derived]` |
| Barb height y | 0.8 mm per side | `[judgment]`; limit is y at most 1.09·eps·L²/h, which is 1.7 mm for PETG one-time, 3.6 % |
| Strain at assembly | barbs squeeze 0.55 mm per side to clear the 6.5 mm neck (barb span 7.6 mm), about 1.1 % strain; well under the 3.6 % one-time and 2.1 % repeated PETG limits | `[derived, fundamentals §4]` |
| Barb lead-in face | 30 degrees from the axis | `[source: Bayer]` |
| Barb catch face | 90 degrees, square, never chamfered (a chamfer becomes a release ramp) | `[source: Fictiv, BASF]` |
| Catch bearing overlap | y minus radial clearance = 0.8 - 0.25 = 0.55 mm (at least 0.5) | `[judgment]` |
| Prong root fillet | at least 0.9 mm (0.5 x h, never below 0.38) | `[source: Hubs, Bayer]` |
| **Counterbore diameter (relief behind the neck)** | **8.6 mm**: the larger of spring OD + 0.5 and neck Ø 6.5 + 2 x 0.8 + 0.5 = 8.6, equal to neck radius + y + 0.25 so the prongs relax fully and never rub | `[source: Bayer stress-free rule; margin judgment]` |
| **Counterbore depth** | Li + travel + barb length + 1 mm, which is 14 + 3 + 1.2 + 1 = **19.2 mm** for the example spring | `[judgment]`; deliberately conservative, trim once the test print works |
| **Spring bore** (spring OD + 0.35 to 0.6 mm diametral) | the counterbore (8.6 mm) is wider than the spring needs, so add a guide pin on the counterbore floor, 1.5 mm diameter, which is at most the Lee rod rule and fits inside the 1.9 mm slot. If your spring OD is 6.0 mm or more, use spring OD + 0.5 as the counterbore instead of a pin | `[source: Lee; judgment]` |
| Spring OD growth | check OD at installed length against the bore; coils swell slightly when compressed | `[source: Lee]` |
| Spring seat | flat shoulder at the prong tips so the end coil bears on both tips and cannot enter the slot | `[judgment]` |
| Preload | 15 to 25 % of (free minus solid); never beyond 85 % in service | `[judgment]` |
| Outer shoulder (hard stop) | on the plunger, larger than the neck; set the gap between shoulder underside and housing face to the 3.0 mm travel so the user cannot bottom the spring | `[judgment]` |
| Detent nose | hemispherical, radius 1.5 mm (plunger radius / 2), 30 to 45 degree ramps | `[judgment; Bayer]` |
| Knob pocket | 1.5 mm deep (half the 3 mm travel, the rest is surface-gap margin), width = nose width + 0.6 mm = 3.6 mm, matching ramps | `[judgment]` |
| Neck mouth | 0.5 mm x 45 degree chamfer; catch step stays square | `[judgment]` |
| Material and walls | PETG, 3 perimeters, 0.2 mm layers, 0.4 mm nozzle | `[source: fundamentals §4]` |

Mark every `[judgment]` value as needing one test print.

## Print orientation

- **Plunger:** print it on its side, with the slot plane **perpendicular to the bed**, so the two prongs sit left and right of the slot and bend within each layer. Upright, each prong is a Z cantilever and snaps along a layer line `[video]`. Slot parallel to the bed makes the upper prong a bridge. Put a flat on the bed side with chord at least 0.4 x 6 = 2.4 mm so the bed edge stays within 45 degrees `[derived]`, and chamfer bed-touching edges 0.4 to 0.6 mm at 45 degrees (elephant foot) `[video; judgment]`. Mirror the flat in the neck bore so the plunger cannot rotate and the barbs always meet the catch.
- **Housing:** print with the bore axis **horizontal** and teardrop sections so the stepped bore needs no support `[video, Hubs]`. If the bore must be vertical, print open end down so the catch step faces up. Either way the catch step is 1.05 mm radial; do not chamfer it.

## CAD steps

1. Housing: bore the 6.5 mm neck (with flat), 10 mm long, chamfer the mouth 0.5 x 45 degrees.
2. Behind the neck, cut the 8.6 mm counterbore to depth (Li + 3 + 1.2 + 1). Leave the step square. Add the 1.5 mm guide pin on the floor if the spring is small.
3. Plunger, outside in: hemispherical nose (R 1.5), outer shoulder, 6 mm sliding body with flat, split zone with a 1.9 mm slot and tapered prongs 9 mm long, barbs (0.8 mm, 30 degree lead-in, 90 degree catch), spring-seat shoulder at the tips, 0.9 mm root fillet.
4. Knob: add the 3.6 mm wide, 1.5 mm deep pockets with 30 to 45 degree ramps matching the nose.
5. Assembly order: drop the spring into the counterbore first, then push the plunger in from outside until the barbs click.

## Tuning

- **Weak return or weak click:** stiffer spring, nest two, or add preload (within 15 to 25 %).
- **Plunger sticks:** raise bore clearance to 0.3 per side, confirm the flat is present, check the bore for ooze blobs.
- **Plunger pops out or sloppy stop:** barb height too small (needs at least clearance + 0.2 mm) or catch face chamfered; reprint.
- **Prong snapped on insertion:** printed upright; reprint on its side.
- **Spring buckles or rubs:** free length over D above 4; trim or use the guide pin.
- **Barbs creep (rub in counterbore):** counterbore too small; keep radius at neck radius + y + 0.25 mm.
- Print one test coupon first: the neck and counterbore section of the housing plus one plunger, about 25 mm long, to confirm bore fit and barb snap before printing the full fixture.
