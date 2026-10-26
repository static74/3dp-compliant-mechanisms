# Redesign: one snap lid that fits an MK4 in PLA and a Bambu in PETG

## What went wrong and what to do instead

Your lid fits by clearance, so the fit depends on each printer's dimensional growth and each material's stiffness. Tuning that clearance for one machine breaks it on the other. The fix is to stop relying on a rigid fit. Use a **grip-fin plug lid**: a plug with 56 thin slanted fins. Each fin is a small in-plane cantilever that bends to absorb whatever the printer's error is. I chose it over a single latch or two side springs because the fins are redundant and each sees the same small strain, so the lid tolerates printer error in both directions. A fin bends about 1.4 times the interference (1/cos 45°). That is why the strain check below uses 0.707 mm.

I do not know your box walls or opening size, so I assume a 60 x 40 mm outside, 2.4 mm walls, and an inside opening of **55.2 x 35.2 mm** at the lip. Replace O_x = 55.2 and O_y = 35.2 with your real inside dimensions. The formulas below follow from them. The box wall at the lip should be at least 2.4 mm. If it is thinner, thicken it at the lip.

## Parameters

| Feature | Value | Tag |
|---|---|---|
| Flange (sits on box rim) | 60 x 40 mm outside, 3 mm thick, R5 vertical corners | `[judgment]` |
| Plug height above flange | 8 mm | `[judgment]` |
| Rigid rail, bottom of plug | lowest 1 mm, full perimeter | `[source: Slant; judgment]` |
| Relief gap above the rail | 0.3 mm (cut under all fin bases) | `[video]` |
| Fin free height | 8 - 1 - 0.3 = 6.7 mm | derived |
| Rail and corner-block size | opening minus 0.6 mm overall, i.e. 0.3 mm clearance per side: 54.6 x 34.6 mm | `[judgment]` |
| Corner blocks | solid, 5 mm along each side from the corner, no fins in the arc | `[measured]` |
| Fin outer envelope | opening plus 0.6 mm overall: 55.8 x 35.8 mm, so 0.3 mm interference per side. Each fin tip stands 0.6 mm proud of the corner-block face | `[judgment]` |
| Fin angle to the wall, phi | 45 degrees | `[judgment]` |
| Fin thickness, t | 0.86 mm (two perimeters) | `[source: Prusa]` |
| Slit width, g | 0.9 mm | derived |
| Pitch along the wall, p | (0.9 + 0.86) / sin 45 = 2.5 mm | derived |
| Fin length, L (root to contact) | 13.5 mm | derived from the PLA sustained limit |
| Slit depth into plug | L sin 45 = 9.5 mm, plus a 1 mm land, so 10.5 mm of solid plug behind each wall | derived |
| Fin count | long sides: (55.2 - 10) / 2.5 = 18 each; short sides: (35.2 - 10) / 2.5 = 10 each; 56 total | derived |
| Fin tops | 0.5 to 1 mm rounded lead-in | `[measured]` |
| Slit ends | R1 fillet at the fin root | `[video]` |
| Bed-side edges | 45 degree chamfer, 0.5 mm, on the flange underside | `[video; size judgment]` |

Slits from opposite sides each reach 9.5 mm into a 17.6 mm half-width, which leaves a 16 mm solid core on the 35.2 mm direction, so they do not collide.

## Why these numbers hold on both printers

Assume printer error of plus or minus 0.2 mm per side `[judgment]`.

- Worst tight case (+0.2): the rigid rail and corner blocks still clear (0.3 - 0.2 = 0.1 mm), so the lid does not bind. Seated interference is 0.5 mm, so a fin deflects 0.5 / cos 45 = 0.707 mm. Strain is 1.5 x 0.707 x 0.86 / 13.5^2 = **0.50 %**. That equals PLA's sustained limit (0.5 %), and PETG's limit is 1.0 %.
- Worst loose case (-0.2): interference is 0.1 mm, so the lid still grips, only lightly.
- Insertion strain stays well under the 1.2 % repeated-snap limit for PLA.

If you shorten the fins to 10.5 mm, you get a PETG-only design (about 0.83 % at the tight case, which fails PLA's 0.5 % sustained limit). Keep 13.5 mm because you need one file for both materials.

## Print orientation

- **Flange down on the bed, plug pointing up.** The fin profile lies in the XY plane, so bending runs along the deposited lines and not across layer interfaces. A fin built up in Z would snap along a layer line.
- Layer height 0.2 mm (anything up to 0.3 mm works with the 0.3 mm relief). Do not exceed 0.3.
- No supports. The first layer of each fin spans the 0.3 mm relief, anchored where the fin meets the plug body, like a support interface. It prints because the gap is small.
- Keep the slicer's default thin-wall handling. Set elephant-foot compensation to about 0.2 mm.
- Before you print a batch, look at the sliced first fin layer once to confirm the slits and the relief survived.
- Do not change the slicer settings per printer or per filament. If you must edit settings to make it fit, the geometry is wrong.

## CAD steps (Fusion)

1. Sketch the 60 x 40 flange with R5 corners, extrude 3 mm. Chamfer the bottom edge loop 0.5 mm.
2. On the flange top, sketch the rail outline (54.6 x 34.6 with the box's inside corner radius) and extrude 8 mm. This is the plug body and the corner blocks.
3. Sketch the fin envelope (55.8 x 35.8) on the plug top face and use it only for placing fin tips. Build one fin: a parallelogram 0.86 mm thick at 45 degrees to the wall, 13.5 mm long, whose outer tip sits on the envelope line and whose root is inside the plug body.
4. Cut one slit of width 0.9 mm beside it, 9.5 mm deep (L sin 45), with a 1.0 mm land behind its inner end. Fillet the root R1.
5. Linear-pattern the fin and slit at 2.5 mm pitch (18 on each long side, 10 on each short side), keeping the 5 mm corner blocks clear. Mirror to the opposite sides.
6. Extrude-cut each fin from the plug top down to 1.3 mm above the flange top. Then cut a 0.3 mm slab under every fin so the fins float above the 1 mm rail.
7. Fillet the fin tops 0.5 to 1 mm. Export STL at fine tessellation and check that the 0.3 mm gap is still open in the mesh. Some exporters close it.

## Test and tune (the `[judgment]` values need one print)

Print one lid in PLA on the MK4 and one in PETG on the Bambu. These values are untested: interference 0.3 mm, rail clearance 0.3 mm, plug height 8 mm, and the flange thickness.

- Too tight on both: lengthen the fins (a longer fin is softer) or cut interference to 0.2 mm.
- Too loose on both: thicken the fins to 3 perimeters (1.27 mm) or raise interference to 0.4 mm. If you raise it, recheck the strain at the tight case.
- Fins fused to the rail: the relief closed. Confirm 0.3 mm in the exported mesh.
- Any fin cracks: you built it across layers or the fins are too thick. Check the orientation.
- Run a 7-day closed test on the PLA lid at your room temperature before you trust it. Accept 20 % force loss or less. Cycle the lid 100 times as well.
- Black PLA and PETG shrink differently, but a 0.2 mm per side difference is already inside the budget above.

This lid does not seal. The slits leave gaps for air and dust.
