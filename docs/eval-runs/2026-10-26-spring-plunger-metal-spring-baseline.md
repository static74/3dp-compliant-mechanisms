# Captive spring plunger for a rotary selector (PETG, Prusa Core One, pen spring)

## The design in one paragraph

The plunger is a 6 mm shank with a wider collar at its back end and a rounded nose at its front. It slides in a stepped bore. The front of the bore is a 6 mm guide hole. Behind the guide hole is a wider chamber that holds the collar and the spring. The collar is wider than the guide hole, so the plunger cannot leave through the front. A separate rear cap closes the chamber, so the plunger cannot leave through the back. The spring sits between the collar and the cap. The collar stops against the front lip at rest and against a hard shoulder at 3 mm of travel, so the spring never goes solid. This design retains the plunger by geometry alone, so no glue or friction is involved.

## Parts

1. Housing: a block, or a pocket in your fixture, with the stepped bore.
2. Plunger: shank, collar and nose in one piece.
3. Rear cap: a plate with a short spigot that centers the spring. Fasten it with two M3 self-tapping screws (about 2.6 mm pilot holes) or heat-set inserts. A press-fit or snap cap is not enough for a "decent force" spring.
4. Spring: one from your bag (selection steps below).

## Starting dimensions (tune with a test coupon)

All clearances are starting values for PETG at 0.2 mm layers on a 0.4 mm nozzle. Print the coupon described below before you trust them.

| Feature | Dimension | Notes |
|---|---|---|
| Plunger shank diameter | 6.0 mm | Nominal |
| Front guide hole diameter | 6.5 mm | 0.25 mm clearance per side. PETG is sticky, so do not go tighter than 0.2 mm per side |
| Guide hole length | at least 8 mm (about 1.3 times the shank diameter) | A short guide lets the plunger cock and bind |
| Collar diameter | 8.0 mm | Retention overlap is (8.0 - 6.5) / 2 = 0.75 mm per side, about two perimeters |
| Collar thickness | 2.5 mm | |
| Chamber diameter | 8.5 mm | 0.25 mm clearance per side to the collar |
| Chamber length | travel + collar thickness + spring length at full compression + any margin | Compute from the spring, see below |
| Nose | hemispherical, radius 2.5 to 3 mm | Or a 5 mm steel ball if you have one, see below |
| Step between guide hole and chamber | 45 degree chamfer | Avoids a flat overhang when printed front face down |

If the spring's outside diameter is more than about 7.6 mm, enlarge the chamber to the spring outside diameter plus 0.6 mm and keep the collar 0.5 mm smaller than the chamber.

## Picking and sizing the pen spring

Pen springs are weak (typically 0.2 to 1 N/mm), so you need to raise the force. Measure first, then adjust.

1. Measure outside diameter, free length and wire diameter with calipers.
2. Measure the rate. Push the spring against a kitchen scale in 1 mm steps and note the grams. Rate in N/mm is (grams / 102) per mm of compression.
3. Choose the force you want at rest and at full travel. A good range for a selector is 3 to 8 N at the detent.
4. Raise the force in one of these ways:
   - Cut the spring shorter with cutters. Rate is roughly inversely proportional to the number of active coils, so half the coils gives about twice the rate. Re-measure after cutting.
   - Add preload. Set the chamber so the spring is compressed 40 to 60 percent at rest. Force is rate times compression, so preload is the cheapest force.
   - Nest two springs of opposite winding (one inside the other) if the diameters allow. Opposite winding keeps them from tangling.
   - Stack identical springs in parallel in separate pockets if the housing allows.
5. Keep the spring at full compression no tighter than about 80 percent of its free length minus solid height. In practice, never let it reach coil-bind. The 3 mm hard stop guarantees this.

Spring length budget (all values in mm):

- Spring length at rest = free length minus preload compression.
- Spring length at full travel = spring length at rest minus 3.
- Spring length at full travel must stay above the solid height plus 1.
- Chamber length from the front lip to the cap face = collar thickness + spring length at rest + 0.3 (clearance).
- The stop at 3 mm: make the cap spigot (or a ledge) stand 3 mm proud of where the collar sits at rest, so the collar hits it at full travel.

Because pen springs vary, treat the numbers above as a procedure. Fix the chamber length after you have measured one spring.

## Making it impossible to fall out

- Front: the collar (8.0 mm) is larger than the guide hole (6.5 mm). The plunger cannot pass forward.
- Rear: the cap is screwed on. The plunger cannot pass backward.
- Spring: the cap spigot and the collar both locate the spring, so it cannot buckle sideways out of the chamber.
- Nose: the nose is part of the plunger and wider than nothing the plunger needs to pass, so it never has to be fitted after assembly. Assemble by dropping the plunger and spring in from the rear, then fitting the cap.
- Service: unscrew the cap to replace the spring.

## Ball option

If you want a true ball detent, use a 5 mm steel ball seated in a spherical pocket in the plunger nose. The front aperture must be smaller than the ball (about 4.2 mm for a 5 mm ball) so the lip captures it. The ball cannot be pressed in after printing, so split the front: make the nose a separate small cap, or fit the ball before the front cap goes on. For a printed hemispherical nose the part count is lower, and PETG against PETG wears slowly at selector loads, so start with the printed nose and move to a ball only if wear or friction is a problem.

## Detent notches on the knob

- Make each notch a shallow spherical or V dimple, 1.5 to 2 mm deep, with flanks about 45 to 60 degrees. Steeper flanks give a stronger click but more wear.
- Nose stroke needs to exceed the notch depth. Your 3 mm of travel gives margin for tolerance and wear.
- The knob face that the nose rides on should be hard and smooth (print the face flat on the bed, or use a metal insert).
- Pitch of the notches sets the angle of each step. Leave at least 2 mm of flat land between notches so the nose does not skip.

## Print settings and orientation

- Material: PETG on the Core One, 0.4 mm nozzle, 0.2 mm layers.
- Housing: print front face down on the bed so the guide hole is round and the chamber opens upward. The 45 degree step avoids support. Add a 0.2 mm chamfer on the guide hole entry to hide elephant foot.
- If the housing is part of a larger fixture and the bore must lie horizontal, make the bores teardrop shaped (point up) and ream the guide hole with a 6.5 mm drill after printing.
- Plunger: print it standing on its collar (axis vertical). The shank is then round and the layer lines run across it, which is fine for sliding.
- Perimeters: at least 4 walls and 40 percent or more infill around the housing, because the cap screws and spring force load the walls. Use 100 percent infill (or just walls) on the plunger.
- Do not print the plunger and the housing in the same job in contact. Leave 5 mm between them.
- Lubricate the shank with a drop of silicone grease. PETG on PETG sticks without it.

## Tolerance test coupon (do this first)

Print one short housing (20 mm tall) with four guide holes at 6.3, 6.4, 6.5 and 6.6 mm, and four plungers at 6.0 mm. Pick the tightest hole where the plunger falls through by gravity when the coupon is held vertical, with no catching. That fit is the right clearance for your printer, filament and slicer. Then size the chamber and collar the same way (0.25 mm per side if the first test confirms 6.5 mm).

## Quick assumptions and checks

- The spring dimensions are unknown until you measure them, so the chamber length is a procedure, not a fixed value.
- The clearances are conservative starting values, not guaranteed. Confirm them with the coupon.
- Check the force against the scale after assembly: push the nose to 3 mm and read the force. Adjust by cutting the spring, adding preload, or nesting a second spring.
