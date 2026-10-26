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
| Prong thickness h | (body Ø − slot)/2 at full body diameter (Ø6 with a 1.9 slot gives 2.05 mm); keep the split zone at body diameter so it also guides in the neck | `[judgment]` |
| Prong length L | 8–13 mm, L/h ≥ 6 (worked Ø6 case: 12.5 / 2.05 = 6.1) | `[judgment]` |
| Barb shape | local ears on the two outer prong faces only, each ≤ 2 mm tall along the slot plane, never a full ring: a ring segment beside the slot cannot pass a round neck in the direction that does not flex. Chamfer the ear z-faces 45° | `[derived]` |
| Barb height y and squeeze | y is measured from the body surface (ear span = body Ø + 2y); squeeze per prong = the x-travel that puts the whole ear inside the neck circle, ≈ (ear span − neck Ø)/2 at the ear's mid-height and a little more at its edges; must satisfy ε = 1.5·squeeze·h/L² ≤ one-time strain (PLA 2 %, PETG 3.6 %). Worked Ø6 case: span 7.6, neck 6.5, ears |z| ≤ 1, squeeze 0.6, h 2.05, L 12.5 → 1.2 % | `[derived from Bayer]` |
| Bearing overlap on the catch face | (barb span − neck Ø)/2, ≥ 0.5 mm (FDM rounds edges); Ø6 case 0.55 | `[judgment]` |
| Slot between prongs | ≥ 2 × squeeze + 0.3 mm so both prongs close fully before touching; Ø6 case ≥ 1.5, use 1.9 | `[derived]` |
| Prong root fillet | ≥ 0.5·h, ≥ 0.38 mm | `[source: Hubs, Bayer]` |
| Counterbore diameter | max(barb span, spring OD, any cap) + 0.5 mm so the prongs relax fully and never rub (a rubbing barb creeps); Ø6 case 7.6 + 0.5 → 8.6 after the printed-hole allowance | `[source: Bayer stress-free rule; margin judgment]` |
| Cavity depth | barb length + installed spring length, measured from the catch step; inward travel is limited by the plunger's outer shoulder, and installed length − travel must stay ≥ solid height + 1 mm | `[derived]` |
| Plunger body clearance | 0.2–0.3 mm per side | `[source: Fictiv; judgment]` |
| Prong width (in Z) | ≥ 5 mm where possible; on a Ø5–8 mm plunger it equals the diameter, accept and test | `[source: Hubs]` |
| Retention check | spring rate × max compression ≪ barb shear force | `[judgment]` |

Orientation (decides everything): print the plunger lying on its side with the slot plane perpendicular to the bed, so the prongs sit left and right of the slot and flex within each layer. Upright, each prong is a Z cantilever and snaps along a layer line `[video]`. Slot parallel to the bed, the upper prong prints as a bridge. Add a flat on the bed side with chord ≥ 0.71·D (depth 0.15·D) so the bed edge stays at or under 45°, and a matching flat in the bore so the prongs always meet the catch and cannot rotate `[derived; judgment]`. If the housing prints bore-up, the catch step is a downward annular overhang: keep it ≤ 1 mm radial or print the housing bore-horizontal; do not chamfer it.

Feature order along the plunger, outside in: detent tip, outer shoulder (stops over-insertion), sliding body, split zone, barbs. Spring seat: choose a spring whose mean diameter lies between the slot width and the plunger diameter so the end coil bears on both prong tips; insert the spring first, then the plunger.

## B. Slicer pause with the spring sealed in `[source: Prusa KB, Cura script, RepRap wiki]`
Model the spring cavity so its top sits exactly on a layer boundary; pause at the first roof layer; drop in the spring and any cap or plunger; resume.

Sealing the spring does not by itself retain a moving plunger, so the plunger needs a collar and the housing an aperture, and the plunger must not stand above the pause layer or the nozzle hits it. The arrangement that satisfies both `[judgment]`:
- Print the housing with the **aperture face down**. The first layers form the aperture plate (thickness ≥ 1.2 mm, aperture Ø = plunger Ø + 0.5 mm). Stand the housing on a rim or feet so the aperture face is recessed above the bed by the plunger's rest protrusion + 0.5 mm; otherwise the nose has nowhere to go.
- Chamber Ø ≥ max(collar, spring OD, cap) + 0.5 mm, because the collar and cap are dropped in through it; a Ø6 plunger with a Ø8.5 collar needs a Ø9 chamber whatever the spring is.
- A free spring under a bridged roof leaves a dead zone: the plunger would move through the head-room before the spring engaged, and nothing would return it through that gap. So capture the spring **preloaded under a bayonet cap**. Datums from the plate's inner face (Z = 0): lip tabs occupy Z = h_lip … h_lip + 1.0 (two tabs at 12 and 6 o'clock, each 0.6 mm inward, 3 mm wide, printed before the pause); cap top = h_lip (it bears on the tab undersides); cap underside = h_lip − t_cap; collar occupies 0 … t_collar; installed spring length Li = h_lip − t_collar − t_cap, so choose h_lip for 15–25 % preload. Roof underside = h_lip + 0.2 (one 0.2 mm layer of head-room above the cap; the tabs, 1.0 mm tall, simply merge into the roof). The pause layer is the first roof layer, bottom at h_lip + 0.2, slider reading h_lip + 0.4; the nozzle passes 0.2 mm above the cap. That first layer bridges the Ø9 chamber over a 0.2 mm gap and may sag onto the captive cap; that is harmless but nothing relies on it.
- Assembly path through the tabs: the collar is oblong, 8.5 mm across the flex-free axis and 7.6 mm across the tab axis, so it drops through the 7.8 mm opening between the tabs when the housing flat keys its orientation; aperture overlap stays ≥ 0.55 per side on every axis. The cap body is Ø7.4 with two ears to Ø8.6 at 3 and 9 o'clock: lower it with the ears in the gaps, press it 1 mm below the tabs against the spring, twist 90° so the ears sit under the tabs, release. No compliant feature or insertion strain is needed. Positive anti-rotation: each tab underside carries a 0.3 mm deep pocket the width of an ear; the spring preload seats the ears in those pockets after the twist, so the cap cannot rotate back without being pressed down first `[judgment]`.
- Return force at the outward stop is the preload, not zero, and there is no dead zone because the spring is always between the collar and the fixed cap.
- Alternative when the plunger axis can be horizontal: print the cavity sideways with a teardrop section and the aperture in a side wall; the plunger then lies flat below the pause layer and nothing protrudes.

| Parameter | Value | Tag |
|---|---|---|
| Cavity top Z | first-layer height + n × layer height (snap to a boundary; mid-layer slicing otherwise shifts it a layer) | `[source: PrusaSlicer slice_z]` |
| Pause layer | the first roof layer = cavity top + one layer height | `[derived]` |
| Head-room | spring top and cap ≥ 0.3–0.5 mm below the cavity top, or the nozzle hits it and the first bridge layer droops onto it | `[source: Prusa KB magnets; margin judgment]` |
| Chamber height stack (plate to roof underside) | h_lip + 0.2 mm (one layer), where h_lip = t_collar + Li + t_cap and h_lip is snapped to a layer boundary; add the spring's free-length tolerance (±0.46 mm on LC 016A) to the preload margin | `[source: Lee; stack judgment]` |
| Spring compressed at capture | only under a bayonet cap locked beneath pre-printed tabs; never pushing on the wet roof | `[judgment]` |
| Chamber diameter | max(collar, spring OD, cap) + 0.5 mm diametral; spring-only cavities with no moving plunger may use spring OD + 0.35–0.6 | `[judgment]` |
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
