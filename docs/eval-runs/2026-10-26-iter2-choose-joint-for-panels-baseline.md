# Joint for a 3-section, 400 mm PLA shelf bracket

## Recommendation

Use a **tapered (wedge) sliding dovetail** with a **small printed snap detent** at the end of travel. A tapered dovetail suits several printers because it does not depend on one fixed clearance. The parts slide freely at first, then wedge tight at the end of the slide, so printer-to-printer tolerance differences only change how far the parts travel before they lock. The detent keeps the sections from backing out.

Sections: 3 pieces of about 135 mm each (the joints add overlap, so each piece prints well under the 250 mm bed). Put the two joints in the straight arm, away from the corner where bending stress peaks, or reinforce the corner and keep the joints in the low-moment region.

## Dimensions (starting values)

| Feature | Value |
|---|---|
| Dovetail flank angle | 45 degrees from the slide axis, so flanks need no support when printed flat (use 50-60 degrees if you print the dovetail upright) |
| Dovetail depth (height of the wedge) | 8 mm |
| Neck width at the root | 14 mm |
| Head width at the tip | 14 + 2 x 8 x tan(45) = 30 mm (reduce to about 24 mm if the bracket arm is narrow) |
| Engagement length | 40 mm per joint |
| Taper along the slide | 1:40 on width (about 1.4 degrees per side), male narrower at the entry end |
| Entry clearance per side | 0.4 mm at the open end, closing to about 0 to 0.1 mm interference at the stop |
| Hard stop | Solid 3 mm wall at the end of the female pocket |
| Corner radius inside the female pocket | 0.5-1 mm; chamfer the male lead-in 1 mm |

The taper turns 40 mm of travel into roughly 1 mm of total width change. That range covers the difference between a printer that over-extrudes by 0.1 mm and one that under-extrudes by 0.1 mm per wall.

## Detent

- Add a cantilever tongue in the female part: 25 mm long, 2.4 mm thick (6 perimeters at 0.4 mm lines, so the tongue is solid), 8 mm wide, cut free on three sides with a 0.8 mm slot.
- Put a 0.8 mm tall, 45 degree-ramped bump on the tongue and a matching 1.0 mm deep, 1.2 mm wider pocket in the male part. The ramp on the entry side is 30 degrees, the back side is 60-90 degrees, so assembly is easy and removal needs deliberate force.
- Print the tongue so its length runs along the layers (XY plane), not across them. Layer lines running along the tongue make it strong when flexed.
- Keep the tongue's deflection (0.8 mm over 25 mm) well below PLA's strain limit of about 2 percent; this design stays near 0.5 percent.

## Print orientation and settings

- Print each dovetail with the sliding axis flat on the bed (the wedge profile lies in the XY plane, and the part is extruded along the slide direction in X or Y). That gives accurate flanks and layer lines that run along the load path.
- Walls: at least 4 perimeters (0.4 mm nozzle) with 40 percent or more gyroid or cubic infill. Joint regions should be almost all perimeters.
- Layer height 0.2 mm, same on every printer. Agree on one slicer profile at the makerspace. The nozzle diameter should also match (0.4 mm).
- Use a 0.15 mm elephant-foot chamfer on bed-contact edges, or enable elephant foot compensation. Elephant foot is the most common cause of a joint that fits on one printer and binds on another.
- Do not print the three sections in different materials or colors of unlike shrink rate, since PLA brands differ by a few tenths of a millimeter.

## Make it work across printers

1. Print one test coupon (male and female, 40 mm long) on every printer you plan to use. It takes about 20 minutes.
2. Check that each coupon slides on by hand for the first 30 mm and locks in the last 10 mm. If it locks too early, add 0.1 mm to the female width; if it never locks, subtract 0.1 mm.
3. If printers disagree by more than 0.3 mm, set one printer as the source for all female halves and let others print the male halves, since matching a pair from the same printer is more reliable.
4. Orient the finished bracket so the shelf load pushes the dovetail into its seat, not out of it. The load should never be along the slide axis.

## Why not the alternatives

- **Straight tongue and groove with friction fit:** it needs a precise clearance (about 0.15 mm), and it changes with every printer. It will be loose on one machine and jammed on another.
- **Round pin and hole:** pins print weakly across layers and give no resistance to bending in a shelf bracket.
- **Dovetail with a constant (untapered) fit:** it works if the clearance is perfect, but it relies on the same tuning, so it fails the multi-printer requirement.
- **Snap-fit only:** a snap detent alone would not carry bending loads from a shelf; the dovetail takes the load and the snap only keeps it assembled.

## Strength note

PLA creeps under steady load, particularly in a warm room or near a window. If the shelf holds heavy items, add one M4 screw through the overlap of each joint as insurance. A shelf load is a long-term static load, so test with about twice the intended weight for 24 hours before trusting it.
