# Redesign: grip-fin lid for the 60 x 40 mm enclosure

## Mechanism and why
Use the **grip-fin lid** (compliant-lids.md, mechanism D, the skill's default removable lid). Your lid fails because it relies on a fixed clearance. Clearance moves with filament, machine and material, so the same file is tight on your MK4 and loose on the Bambu in PETG. A grip-fin lid carries a rigid locating plug plus a ring of slanted in-plane cantilever fins. The fins accept a range of plug sizes and spring back, so one file serves both printers. This is the Slant 3D method: do not tune clearance, make the geometry flex. It also needs no metal spring.

I chose the "strain-safe" fin recipe, not Slant's thicker fins. PLA creeps under sustained preload, and a lid sits closed for months.

## Assumptions (replace with your numbers)
- 60 x 40 mm is the box outside size. Wall 2.4 mm (6 perimeters at 0.4 mm). So the opening is **55.2 x 35.2 mm**, vertical corners R5 outside (R2.6 inside; use the real inside radius).
- Fins need something to press on, so walls must be at least 2 mm. The lid does not seal; fins leave gaps.
- 0.4 mm nozzle, 0.2 mm layers. If your wall differs, change only "Opening" and the fin counts; every other value stays.

## Parameter table
| Parameter | Value | Tag |
|---|---|---|
| Lid flange (outer) | 60 x 40 x 3 mm, R5 corners | [judgment] |
| Plug height above flange | 8 mm (≥ 7 mm free fin height) | [measured, scaled from Slant's 8 mm] |
| Opening (box inside) | 55.2 x 35.2 mm | your box |
| Plug nominal size (before slits) | opening + 2 x 0.25 = **55.7 x 35.7 mm** (0.25 mm interference per side; 0.5 only for PETG lids opened often) | [judgment] |
| Plug corners | solid R5 blocks, no fins through the arc | [measured] |
| Slit width | 0.5 mm | [video on screen] |
| Fin thickness | 0.86 mm (two perimeters) | [source: Prusa KB; derived] |
| Slit angle | 30 degrees from the wall (fins lean, never radial) | [derived] |
| Slit length | 9.5 mm (depth into plug about 4.75 mm) | [derived, strain <= 0.5 %] |
| Pitch along the wall | 2.8 mm | [derived from 0.86 + 0.5 and 30 degrees] |
| Fins, long side (55.7 mm minus two 5 mm corner blocks) | about 16 per side | derived |
| Fins, short side (35.7 mm minus corners) | about 9 per side | derived |
| Fin free height | about 7 mm | [measured] |
| Bottom relief under fins | **0.3 mm** slab removed (0.3 min, 0.5 max) | [video XKrDUnZCmQQ; PrusaSlicer slice_z] |
| Rigid locating base | keep the lowest 1 mm of plug unslit (the fins end 0.3 mm above flange; see CAD step 6) | [video] |
| Fin tip | rounded or chamfered lead-in, 0.5-1 mm | [measured] |
| Flange and plug-top edges | 45 degree chamfer 0.5 mm on bed-side edges; 2 mm fillet on plug top | [video; size judgment] |

Strain check (PLA): tip travel perpendicular to the fin is 0.25 x cos30 = 0.22 mm. Strain = 1.5 x y x t / L^2 = 1.5 x 0.22 x 0.86 / 9.5^2 = about 0.31 %. That is under the 0.5 % sustained-preload limit for PLA and well under PETG's 1.0 %.

Every [judgment] value (flange thickness, 0.25 mm interference, edge chamfers) needs one test print.

## Print orientation
- **Flange down on the bed, plug pointing up.** Every fin profile then lies in the XY plane, so bending runs along the deposited lines. A fin built up in Z snaps along layer lines.
- Layer height 0.3 mm or less; 3 perimeters; no supports; keep Arachne and thin-wall detection at defaults (fin thickness is already a whole perimeter multiple).
- 45 degree chamfer on the flange's bed-side edge, elephant-foot compensation about 0.2 mm, so the first layer does not flare.
- Mount the box the usual way (opening up). The box needs no change beyond a smooth, straight inner wall.

## CAD steps (Fusion)
1. Sketch the 60 x 40 flange, R5 corners, extrude 3 mm. Chamfer the bottom edge loop 0.5 mm at 45 degrees.
2. On the flange top, sketch the plug at 55.7 x 35.7 mm with corner radius matching the box inside radius plus 0.25 mm. Extrude 8 mm. Fillet the top edge 2 mm.
3. On the plug top face, sketch one slanted parallelogram along a long edge: 0.5 mm wide, 9.5 mm long, 30 degrees from the wall, starting so the slit opens at the wall. Keep a 5 mm solid corner block at each end.
4. Linear-pattern it at 2.8 mm pitch (about 16 on long sides). Copy to the short sides (about 9). Circular or mirror-pattern for the opposite sides, skipping the corners.
5. Extrude-cut the slits down the plug, stopping at the flange top.
6. Cut a 0.3 mm slab from the fin bases so the fins float above the flange. Retain the solid 1 mm rigid base at the bottom of the plug for alignment, below the fins' free length.
7. Fillet the fin tops 0.5-1 mm (lead-in).
8. Export STL at fine tessellation. Open it in the slicer and check the 0.5 mm slits and the 0.3 mm gap survived; exporters sometimes close them.

## Tuning (one test print, then lock the file)
- Print the lid in PLA on the MK4 and in PETG on the Bambu. Do **not** adjust per printer.
- Too stiff on both: lengthen slits or thin fins. Too loose on both: raise interference to 0.3 mm per side or thicken fins.
- Lid loosens over weeks in PLA: that is creep; PETG or ASA, or longer and thinner fins.
- Fins fused to the flange: the 0.3 mm relief closed; check the mesh.
- A fin snaps: it was built vertically or the slit is too short.

## Scope note
These numbers are FDM starting points. Strain limits come from datasheets with moulded-plastic snap-fit rules, not from printed-beam tests.

SKILL FEEDBACK: The routing worked, and the lids file's strain-safe fin recipe was the right one, but I had to derive the 60 x 40 values myself. The recipe gives fin thickness, pitch and slit length without saying how pitch follows from slit width, fin thickness and angle (I worked out 2.8 mm at 30 degrees), and the "35 fins" and "1.9 mm pitch" belong to the 85 mm part. A scaling rule or small worked example for non-square or small lids would help. The "rigid locating base" instruction is vague about its height, and the relief cut makes it conflict with "slits stop at flange top"; I picked 1 mm unslit base but flagged it unclear. The skill gives no wall-thickness guidance, so I had to assume 2.4 mm. The per-side interference of 0.2-0.3 versus 0.5 is hard to apply with no tie to material. fundamentals.md §12 asks for "CAD steps", but compliant-lids.md "Model" lines are terse for fins. No contradictions beyond the base/relief point.
