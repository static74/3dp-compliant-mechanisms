# Capturing a metal spring: two methods

Every metal-spring mechanism uses exactly one of these. Say which, and why.

| | A. One-way barbed plunger | B. Slicer pause, spring sealed in |
|---|---|---|
| Assembly | drop spring in the bore, push plunger in from outside; barbs snap behind the neck and can never back out | print pauses at the cavity-roof layer, you drop in the spring (and cap/plunger), print resumes and closes the cavity |
| Parts | housing + plunger, both printed separately | one print, plus the spring |
| Serviceable | no (90° catch) unless you add a release window | no |
| Risk | prong snaps if printed in the wrong orientation | nozzle hits a proud spring; roof sags; pause misplaced by a layer |
| Pick when | the user prints parts on any machine and assembles by hand; multiple plungers | the user controls the slicer; the cavity must be fully enclosed; a printed spring is impossible but the mechanism must be one piece |

## A. One-way barbed plunger `[source: Bayer, Fictiv, Hubs; values tagged]`
The plunger's inner end is split into two cantilever prongs, each ending in a barb with a 30° lead-in face and a 90° catch face. The housing bore has a narrow neck at the outer face and a wider counterbore inside. Pushing the plunger in from outside compresses the prongs through the neck; once the barbs pass, they spring open into the counterbore and their 90° faces catch on the inner side of the neck. The spring, seated on the prong tips, pushes the plunger outward only as far as the catch. Nothing short of shearing the barbs removes it.

| Parameter | Value | Tag |
|---|---|---|
| Lead-in face angle | 30° from the axis (20–45°) | `[source: Bayer]` |
| Catch face angle | 90°; never chamfer it, a chamfer turns it into a release ramp | `[source: Fictiv, BASF]` |
| Prong thickness h | 1.0–1.5 mm (2–3 perimeters), tapered toward the barb | `[judgment; taper source: Bayer]` |
| Prong length L | 8–12 mm, L/h ≥ 6 | `[judgment]` |
| Barb height y | y ≤ 0.67·ε·L²/h (×1.6 if tapered): L 8, h 1.2 → 0.7 mm PLA, 1.3 mm PETG one-time | `[derived from Bayer]` |
| Bearing overlap on the catch face | barb height − radial body clearance, ≥ 0.5 mm (FDM rounds edges) | `[judgment]` |
| Slot between prongs | ≥ 2·y + 0.3 mm so both close fully | `[derived]` |
| Prong root fillet | ≥ 0.5·h, ≥ 0.38 mm | `[source: Hubs, Bayer]` |
| Counterbore radius | neck radius + y + 0.2–0.3 mm so the prongs relax fully and never rub (a rubbing barb creeps) | `[source: Bayer stress-free rule; margin judgment]` |
| Counterbore length | plunger travel + barb length + margin, so barbs never hit the floor before the spring goes solid | `[judgment]` |
| Plunger body clearance | 0.2–0.3 mm per side | `[source: Fictiv; judgment]` |
| Prong width (in Z) | ≥ 5 mm where possible; on a Ø5–8 mm plunger it equals the diameter, accept and test | `[source: Hubs]` |
| Retention check | spring rate × max compression ≪ barb shear force | `[judgment]` |

Orientation (decides everything): print the plunger lying on its side with the slot plane perpendicular to the bed, so the prongs sit left and right of the slot and flex within each layer. Upright, each prong is a Z cantilever and snaps along a layer line `[video]`. Slot parallel to the bed, the upper prong prints as a bridge. Add a flat on the bed side and a matching flat in the bore so the prongs always meet the catch and cannot rotate `[judgment]`. If the housing prints bore-up, the catch step is a downward annular overhang: keep it ≤ 1 mm radial or print the housing bore-horizontal; do not chamfer it.

Feature order along the plunger, outside in: detent tip, outer shoulder (stops over-insertion), sliding body, split zone, barbs. Spring seat: choose a spring whose mean diameter lies between the slot width and the plunger diameter so the end coil bears on both prong tips; insert the spring first, then the plunger.

## B. Slicer pause with the spring sealed in `[source: Prusa KB, Cura script, RepRap wiki]`
Model the spring cavity so its top sits exactly on a layer boundary; pause at the first roof layer; drop in the spring and any cap or plunger; resume.

| Parameter | Value | Tag |
|---|---|---|
| Cavity top Z | first-layer height + n × layer height (snap to a boundary; mid-layer slicing otherwise shifts it a layer) | `[source: PrusaSlicer slice_z]` |
| Pause layer | the first roof layer = cavity top + one layer height | `[derived]` |
| Head-room | spring top and cap ≥ 0.3–0.5 mm below the cavity top, or the nozzle hits it and the first bridge layer droops onto it | `[source: Prusa KB magnets; margin judgment]` |
| Cavity height, spring free | free length + free-length tolerance (±0.46 mm on LC 016A) + head-room | `[source: Lee]` |
| Spring compressed at capture | do not let it push on the wet roof; drop in a printed cap or plunger held by an already-printed lip or twist-lock, or capture the spring free and compress it later with the plunger | `[judgment]` |
| Cavity diameter | spring OD + 0.35–0.6 mm diametral | `spring-loaded.md` |
| Roof | span ≤ 5 mm bridges without sag; wider cavities get a 45° chamfered or teardrop roof, or a dropped-in cap | `[source: Hubs; video]` |

Per slicer and firmware:
| Slicer | How | Command |
|---|---|---|
| PrusaSlicer (≥ 2.2) | Preview, layer slider to Z = cavity top + h, right-click +, "Insert pause print (M601)", add an LCD message; pause runs before that layer; not with sequential printing | M601 (Prusa/Buddy). Marlin has no M601: use M125 or M0; Klipper PAUSE; RRF M226 |
| Cura | Extensions → Post Processing → "Pause at height"; prefer **By Layer** = last cavity layer number (By Height = cavity top + h, but Z-hop can false-trigger); Reason = "All Others"; Extra Prime ≈ 0.3 mm; check M82/M83 not flipped | M0 Marlin, M25 BQ, M226 RepRap, M125, PAUSE Klipper, @pause Octo |
| Bambu Studio | Preview slider → right-click + → Add Pause; re-slice; may show as a colour-change marker; verify after saving | M400 U1 |
Never use M600 for an insert: it unloads filament.

Document in the design notes, in this order: (1) cavity top Z, (2) pause layer per slicer, (3) pause command per firmware, (4) the LCD insert message ("Drop spring LC 018B 05 S then cap, flat side down. Resume."). Verify: open the G-code, find the pause command, confirm the next layer Z equals cavity top + one layer height.

## Failure modes
- Plunger pops out (A): barb height below clearance + 0.2 mm, or catch face chamfered.
- Prong snapped on insertion (A): printed upright; reprint on its side.
- Nozzle knocked the spring (B): no head-room, or spring proud; recess 0.5 mm.
- Roof collapsed onto the spring (B): compressed spring pushing on the bridge; capture free, or add a cap.
- Pause one layer late (B): re-insert the pause and check the G-code.
