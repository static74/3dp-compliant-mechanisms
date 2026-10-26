# Redesign: one 60 x 40 mm snap lid that fits PLA on an MK4 and PETG on a Bambu

## Mechanism and why

Replace the rigid snap with a grip-fin plug lid (Slant 3D's default removable lid). The question answered here is "how do I stop tuning a clearance per filament and printer?" Your lid is tight in PLA and loose in PETG because it relies on a fixed clearance, and that clearance moves with filament, machine and slicer. Grip fins make the plug's outer perimeter slightly larger than the opening, and each slanted fin bends in the XY plane to absorb whatever the printer did to the size. About 64 fins share the load, so one printer's error shifts the grip a little instead of deciding between "stuck" and "falls off". In short: use fins that flex, not a gap that must be right.

## Assumptions (change these and rescale)

- The box opening is 60.0 x 40.0 mm, with inside corner radius R3.
- The box wall is 2.4 mm or thicker (6 perimeters). Fins need that wall to press against. Below 2 mm, this mechanism is the wrong choice.
- The lid is separate and flange-down, with a flange flush with the box outside.
- Your PLA and your coworker's PETG both use 0.4 mm nozzles and 0.2 mm layers.

If the true opening differs, keep every number below that is not a length and use the scaling rules at the end.

## Parameters

Sizes in mm unless marked. Tags: [video] stated by Slant 3D, [measured] read from Slant's frames, [derived] calculated from the skill's strain formulas, [judgment] untested engineering judgment.

| Feature | Value | Tag |
|---|---|---|
| Flange | 64.8 x 44.8 x 2.4 (opening plus 2 x 2.4 wall), R5.4 corners, 0.5 mm 45 deg chamfer on the bottom edge | [judgment] |
| Plug height above flange | 10 | [judgment] |
| Plug footprint, corner blocks (rigid locator) | 59.6 x 39.6 (0.2 per side snug clearance), R2.8 corners | [source: snug locating 0.15-0.20] |
| Plug footprint at fin faces (undeflected) | 60.5 x 40.5 (0.25 mm interference per side) | [judgment]; PLA wants 0.2, PETG 0.3, so 0.25 serves both |
| Corner blocks | solid, 4 mm of straight edge from each corner, no fins | [measured] concept, size [judgment] |
| Fin angle to the wall | 45 deg | [derived] strain-safe recipe |
| Fin thickness t | 0.9 (two perimeters) | [derived] |
| Slit width g | 0.9 (safer against fusing than 0.5) | [derived/judgment] |
| Pitch along the wall | 2.5 | (g + t) / sin 45 = 2.55, rounded; [derived] |
| Fins, long sides (60) | 20 per side, spread across the 52 mm between corner blocks | [derived] |
| Fins, short sides (40) | 12 per side, spread across 32 mm | [derived] |
| Slit length (fin free length) L | 9.8 | [derived], from L = sqrt(1.5 t (delta/cos phi) / eps) with delta 0.25, eps 0.5 % |
| Slit depth into the plug | 6.9 (L cos 45), leaving the 26 mm core untouched on the short axis | [derived] |
| Bottom relief under fins | 0.3 mm slab removed under every fin base (never less than 0.3) | [video XKrDUnZCmQQ; PrusaSlicer slice_z] |
| Rigid rail | lowest 1 mm of the plug wall is NOT slit, above the 0.3 relief, if corner blocks do not touch the box | [judgment] |
| Fin top | 0.8 rounded lead-in; 1 mm fillet around the plug top edge | [measured] |
| Pry notch | 3 x 2 mm slot in the flange edge at the middle of one long side | [judgment] |

Strain check: sustained bending strain per fin is about 0.5 % in PLA (the sustained limit) and about half the PETG limit, so PLA is the governing case. Deflection force is roughly 2.3 N per fin in PLA [derived]. Because PETG is less stiff, it grips a little softer than PLA, and 0.25 mm interference keeps that softer grip above "falls off" on a 64-fin lid [judgment].

## Orientation

Print the lid flange down, plug up, on both printers. Every fin, slit and corner block then has its profile in the XY plane and bends along the deposited lines, never across layer interfaces. A fin built on its side would snap along the layer lines.

- Chamfer the flange bottom edge 0.5 mm at 45 deg and keep elephant-foot compensation near 0.2 mm in the slicer.
- 0.2 mm layers (0.3 mm or finer is fine with the 0.3 mm relief), 3 perimeters, no supports, no brim.
- Keep the slicer's default thin-wall and Arachne behavior. Do not change flow or compensation to "make it fit"; that defeats the design.
- PETG on the Bambu: use the usual PETG retraction and cooling so the 0.9 mm slits do not string shut. Remove strings with a knife, not by sanding the fin faces.

## CAD steps (Fusion)

1. Sketch the flange 64.8 x 44.8 with R5.4 corners. Extrude 2.4. Chamfer the bottom edge 0.5 mm.
2. On the flange top, sketch the 60.5 x 40.5 fin envelope offset to R3.2 corners. Extrude 10 mm. This is the plug at fin-face size.
3. Cut the corner blocks back: sketch a 59.6 x 39.6 R2.8 rectangle and, for the four 4 mm corner zones only, extrude-cut the plug down to it so the blocks locate at 0.2 mm per side. Leave the rest of the perimeter at 60.5 x 40.5 for the fins to occupy.
4. On the plug top, sketch one slanted parallelogram slit along a long side: 0.9 mm wide, 9.8 mm long, at 45 deg to the wall, entering from the plug edge. Linear-pattern 20 at 2.5 mm pitch starting 4 mm from a corner. Mirror to the other long side.
5. Repeat on a short side with 12 slits at 2.5 mm pitch, then mirror. Keep slit slant direction consistent (all fins lean the same way around the part).
6. Extrude-cut all slits down through the plug to 0.3 mm above the flange top, or to the 1 mm rail height if you want the rail.
7. Cut a 0.3 mm slab under each fin base so the fins float above the flange. Confirm the gap survived when you export the STL; set fine tessellation, because some exporters close a 0.3 mm gap.
8. Fillet the fin tops 0.8 mm and the plug top edge 1 mm. Cut the 3 x 2 mm pry notch.

## Tuning (one test print, then done)

This is [judgment] geometry, so print one lid in PLA on the MK4 and one in PETG on the Bambu before releasing. Then adjust one knob and keep a single file:

- Too tight in both: make slits longer (softer) by 1 mm, or delete every fourth fin. Do not reduce interference below 0.2 mm.
- Too loose in both: make fins thicker to 1.35 mm (three perimeters) and raise the pitch to 3.4 mm, or raise interference to 0.3 mm.
- Tight in PLA, loose in PETG after that: this is the case where the design already splits the difference. Stay at 0.25 mm interference and lengthen fins slightly; do not make two versions.
- If a PLA lid stays closed for weeks and loosens, that is creep; PETG or ASA suits a lid that never comes off. Fins bending sustained above 0.5 % creep in PLA.

## Scaling to a different opening

- Fins per side = (side length - 8) / 2.5, rounded down.
- Corner block length = the box's inside corner radius plus about 1 mm.
- Pitch p = (g + t) / sin phi. At other angles: 30 deg needs L at least 9.5 mm for the same interference; 45 deg needs 9.8 mm.
- Slit depth into the plug = L cos phi, plus a 1 mm land. The plug must be at least that deep on its short axis.
- Fin height = plug height minus the 0.3 mm relief, and at least 5 mm.

## Why this fixes the two-version problem

The rigid corner blocks align the lid within 0.2 mm per side on any printer, and the fins absorb the rest of the size error. Interference of 0.25 mm per side sits between the PLA value (0.2) and the PETG value (0.3), and the fin compliance covers that difference, so the same STL grips both. Verify with the single test print before trusting it.
