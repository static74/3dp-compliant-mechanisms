# Joint for a 400 mm PLA bracket printed in 3 sections

## Recommendation

Use a **tapered (wedge) dovetail slide with a small printed detent bump**, one joint at each of the two seams. Sections are about 134 mm long, so each fits the 250 mm bed with room to spare.

The question is which joint lets three sections slide together, stay put without glue, and still work across several different printers. A tapered dovetail answers it for three reasons:

- The dovetail's angled walls lock the sections against pulling apart sideways and against bending.
- The taper makes the fit self-adjusting. A section that prints slightly large simply stops sliding a few millimetres earlier. A parallel-sided joint would jam or rattle.
- The detent bump stops the sections from sliding back out under vibration or handling.

## Orientation

Print every section flat on the bed. Draw the dovetail profile in the XY plane and extrude it through the part's thickness (Z), so the slide direction is Z. Profile dimensions then depend only on XY accuracy, with no overhangs and no bridging. The slide axis should be the one the shelf load does not pull along, so the load seats the joint instead of pushing it apart.

## Dimensions (0.4 mm nozzle, 0.2 mm layers, at least 3 perimeters)

| Feature | Value |
|---|---|
| Dovetail flank angle | 15 degrees from the slide axis (75 degrees included between flank and face; avoid steeper than about 60 degrees, since it thins the tail) |
| Tail neck width | 10 mm |
| Tail head width | about 16 mm (follows from depth and angle) |
| Depth of dovetail | 8 mm |
| Taper along slide axis | 1 degree per side (about 1.7 mm of total width change over a 50 mm slide length) |
| Clearance at the tight (leading) end | 0.10 mm per side |
| Clearance at the loose (entry) end | about 0.35 mm per side |
| Slide length | at least 40 mm, ideally 50 mm or more |
| Wall thickness around the socket | at least 2.4 mm (6 perimeters at 0.4 mm) |
| Entry chamfer on the socket | 0.8 mm x 45 degrees |
| Detent bump | 0.5 mm high, 3 mm wide, rounded, on the tail flank near the end of travel |
| Detent flexure | slot 1.2 mm wide, 15 mm long, beside the socket wall so the wall flexes |
| Elephant-foot relief | 0.4 mm x 45 degree chamfer on the first layer edges of tail and socket |
| Stop | hard stop at the end of travel so the sections seat flush |

Sections have a tail on one end and a socket on the other. The middle section carries one of each, so all three parts can be assembled in order.

## Why these numbers

- A flank of 15 degrees is steep enough to lock but is printed as a vertical wall, so it does not suffer from overhang droop.
- A clearance range of 0.10 to 0.35 mm per side covers the typical spread between well-tuned and sloppy printers. The taper spends that range along the slide, so each printer finds its own snug point.
- The detent bump of 0.5 mm engages a few tenths of a millimetre of flexure. PLA is stiff and creeps, so keep the bump small and the flexure long. A big bump will crack or take a permanent set.

## Material cautions for PLA

- PLA creeps under steady load. If the shelf carries heavy weight over months, the wedge may slowly seat further and loosen. PETG or an ASA would be more forgiving, but PLA is fine for light and medium loads.
- Keep the part out of hot cars and direct sun. PLA softens around 55 to 60 degrees C.
- Layer lines run across the dovetail neck. Orient the section so the neck is not the weakest direction, and use at least 4 perimeters with 40 percent or more infill near the joint.

## Make it work across printers

1. Print a short test coupon (a 20 mm slice of tail and socket) on each makerspace printer before printing full sections.
2. Calibrate flow and use the same slicer profile if possible. Turn on "arc fitting" off and "coasting" off, since they alter small features.
3. If a printer is too tight, sand or file the tail flanks lightly. If it is too loose, print the socket on that printer with 0.05 mm less clearance or use the other end of the taper.
4. Label each section and each printer used, and keep joined pairs together. Sections from the same printer mate best.

## If the joint feels too loose anyway

Add a thin crush rib (0.3 mm tall, 0.8 mm wide) along one flank of the tail. It deforms on first assembly and takes up printer-to-printer variation.

## Summary

Use a tapered dovetail (15 degree flanks, 10 mm neck, 8 mm deep, 1 degree taper per side, 0.10 to 0.35 mm clearance) with a 0.5 mm detent bump, printed flat so the profile lies in the XY plane. Test a coupon on each printer first.
