# Redesigning the 60x40 mm snap lid so it works on any printer and filament

## Why the current lid fails

Your lid probably does two jobs with one feature: the rim that aligns the lid also provides the snap force. That rim is an interference fit, so the fit depends on a dimension that varies by about +/-0.15 mm between printers and filaments. Over-extrusion, shrinkage and elephant foot differ between your MK4 with black PLA and your coworker's Bambu with PETG. PLA is also about 1.5x stiffer than PETG, so the same interference is a squeeze in one material and a loose lid in the other.

The fix is to split the jobs:

1. **Alignment** uses a deliberately loose lip. A clearance of 0.4 mm per side is sloppy enough that nothing rubs on either printer.
2. **Retention** uses a few long cantilever arms. A long beam turns a +/-0.15 mm size error into only a +/-20% change in force, and the arms are never loaded at rest, so PETG creep does not matter.

## Assumptions (change these to match your box)

- Box wall is 2.4 mm. The inside cavity is 55.2 x 35.2 mm.
- You can add a groove inside the box wall.
- Nozzle is 0.4 mm and layer height is 0.2 mm.

If your wall is thinner than 2.4 mm, add a local 3 mm boss behind each groove.

## Lid dimensions

| Feature | Dimension |
|---|---|
| Lid plate | 60 x 40 x 2.4 mm, outer corner radius matching the box |
| Alignment skirt, outer size | 54.4 x 34.4 mm (0.4 mm clearance per side inside the 55.2 x 35.2 cavity) |
| Skirt wall | 1.6 mm (exactly 4 perimeters) |
| Skirt height above plate | 5.0 mm |
| Corner radius on skirt | at least 2 mm, with 0.5 mm chamfer on the top edge as a lead-in |
| Number of snap arms | 4, two on each long side, placed 12 mm in from each end |
| Arm length (L) | 14 mm |
| Arm thickness (h) | 1.6 mm (4 perimeters, no infill) |
| Arm height | 5.0 mm, full skirt height |
| Arm root fillet | 0.8 mm radius where the arm meets the skirt |
| Slot between arm and plate | 0.6 mm wide, cut through the lid plate |
| Arm slot at free end | 0.8 mm, so the arm can move in-plane |
| Hook nub, protrusion | 1.1 mm beyond the skirt outer face |
| Hook nub, height | 1.6 mm, near the top of the arm, centered 2.5 mm below the skirt top |
| Hook nub faces | 45 degrees on both the lead-in side and the return side |

Each arm is a 14 mm segment of the skirt wall. It is attached to the rest of the skirt at one end only. The plate is cut away behind it so the arm can flex inward in the horizontal plane.

## Matching box feature

Cut a groove into the inside face of the box wall on each long side, in line with each arm.

| Feature | Dimension |
|---|---|
| Groove depth | 1.0 mm into the wall |
| Groove width | 2.2 mm (hook is 1.6 mm, so 0.3 mm slack above and below) |
| Position | Groove centered 3.5 mm below the rim, to match the nub |
| Lower face of groove | 45 degrees, so it prints without support |
| Groove length | 10 mm, centered on each arm |

The nub reaches 0.7 mm into the groove. Dimension errors of +/-0.15 mm leave 0.55 to 0.85 mm of engagement, so the lid always catches.

## Why these numbers hold up on both materials

- **Insertion deflection:** the nub protrudes 1.1 mm and the wall clearance is 0.4 mm, so each arm deflects y = 0.7 mm during insertion.
- **Strain:** for a rectangular cantilever, strain = 1.5 x h x y / L^2 = 1.5 x 1.6 x 0.7 / 196 = 0.86%. Worst case with +0.15 mm error is about 1.0%. PLA tolerates roughly 1.5 to 2% in the XY plane, so the arms will not crack.
- **Force:** F = 3EI y / L^3. With b = 5 mm of arm height, E of about 2 GPa for PLA and 1.4 GPa for PETG, each arm needs roughly 1 N to 2 N to deflect. With four arms and 45-degree faces, the lid takes a deliberate tug to remove and does not fall off. The PLA and PETG forces differ by about 1.4x instead of the large swing you see with an interference rim.
- **Creep:** the arms sit relaxed when the lid is closed, so PETG does not relax over time.

## Print orientation

- Print the lid **outer face down** on the bed, skirt and arms pointing up.
- The arms are walls growing straight up, bending in the horizontal plane. Layer lines therefore run along the arm length, and bending stress runs along the layers, not across them. That is the strong direction. Printing the lid on its side or with the arms bending about a horizontal axis would put the stress across layer lines and the arms would snap.
- No supports are needed. The nub has 45-degree faces and the slots are open to the bed.
- Slicer settings to share with your coworker: 0.2 mm layers, 4 perimeters, 0.4 mm nozzle, no ironing, no "thin wall" detection tricks, seam away from the arms (place it at a corner of the plate). Because the arm is exactly 1.6 mm, it slices to four clean 0.4 mm perimeters on any slicer.
- Elephant foot only affects the outer face and the slot edges at the bed, which is not a mating surface. If your coworker sees a flared first layer, add a 0.2 mm chamfer on the outer lid edge.
- Print the box with the groove face up (open top up). Check that the groove prints cleanly, since the 45-degree lower face is the only overhang.

## Fusion 360 steps

1. Sketch the 60 x 40 plate outline and extrude 2.4 mm.
2. Offset the cavity outline inward by 2.4 + 0.4 mm and extrude the skirt wall (1.6 mm) up 5.0 mm.
3. Sketch each arm as a 14 x 1.6 mm rectangle along the skirt wall. Cut the 0.6 mm slot in the plate behind it and the 0.8 mm gap at the free end.
4. Sketch the nub triangle profile (1.1 mm protrusion, 45 degrees both sides, 1.6 mm tall) on a plane through the arm and extrude it across the arm height. Add the 0.8 mm root fillet.
5. In the box, use a Combine/Cut with a groove sketch on the long inside walls.
6. Define user parameters for clearance (0.4), nub protrusion (1.1), arm length (14) and arm thickness (1.6) so you can tune once and regenerate.

## Validate once, then stop maintaining two versions

Print one lid on your MK4 and one on your coworker's Bambu and try both on the same box printed on either machine. If the lid is too loose on both, raise nub protrusion by 0.2 mm. If it is too tight on both, drop it by 0.2 mm. Do not tune per printer. A lid that works on both with the same file is the goal, and the long arms give you enough margin that you should not need to.
