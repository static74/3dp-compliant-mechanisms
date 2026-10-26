# Captive spring plunger (ball-detent style) for a PETG selector fixture

## Design in one paragraph

Print three parts: a housing with a bore, a plunger with a domed tip and a spring pocket, and a rear plug. The bore ends at the front in a narrower round hole (the lip). The plunger has a wider body (a shoulder) that cannot pass through the lip, so the spring can never push the plunger out. You insert the plunger and spring from the back, then lock the rear plug in place. The plunger is trapped between the lip and the plug.

## Dimensions (starting values, all in mm, for a 0.4 nozzle PETG print)

| Feature | Value | Why |
|---|---|---|
| Plunger body diameter | 6.0 | Your 6 mm requirement |
| Housing bore diameter | 6.4 | 0.2 per side. PETG is sticky and swells at the first layers, so tighter than 0.2 binds. |
| Plunger tip (dome) diameter | 4.4 | Passes through the lip with 0.1 per side clearance |
| Lip hole diameter | 4.6 | Smaller than 6.0 body, so the shoulder is trapped |
| Lip thickness | 1.5 | At least 4 perimeters (1.6 mm) of solid wall around the hole |
| Shoulder overlap | 0.7 per side | (6.0 minus 4.6) / 2. Gives a wide stop face. |
| Plunger body length (shoulder to rear) | 8 | Length/diameter of about 1.3 stops the plunger cocking and jamming |
| Spring pocket in plunger rear | 5.0 diameter by 5 deep | Guides the spring so it cannot buckle sideways |
| Tip protrusion at rest | 2.0 | Detent notch depth should be about 1.5 or less |
| Travel | 3.0 | Tip ends up 1.0 below the lip face when fully pushed in |
| Bore depth, lip inner face to plug face | 16 | See spring budget below |

Add a 45 degree chamfer on the inner side of the lip and under the shoulder so both print without supports. Round the dome tip with a 2 mm radius. Add a 0.3 mm chamfer on the bore entrance so the plunger slides in without catching the elephant-foot ridge.

## Spring budget (works with your pen springs)

Use these three checks on each candidate spring from the bag:

1. **Outer diameter** must be 5.0 to 5.6 mm if it sits in the pocket, or up to 6.0 if it only sits in the bore. Smaller springs: reduce the pocket diameter to the spring's OD plus 0.3.
2. **Free length** (Lf) sets the plug position. The gap between the plunger rear face and the plug face is G = Lf minus preload minus pocket depth. With Lf = 14, preload 1 and pocket 5, G = 8, which gives the 16 mm bore depth above (8 body + 8 gap). Change the bore depth if your spring is different.
3. **Solid height** (coils stacked flat) must be at most Lf minus preload minus travel, minus 10 percent. If the spring bottoms out before 3 mm of travel, the plunger stops hard and the printed parts take the load.

### Getting "decent force" from pen springs

Pen springs are weak. A typical 0.4 mm wire, 6 mm OD, 20 coil spring has a rate of only about 0.07 N/mm. Over 3 mm that is about 0.2 N, which is too light for a selector detent. The rate scales with the inverse of the number of active coils, so you have three levers:

- **Cut coils off.** Cutting a spring from 20 to 5 coils raises the rate fourfold, to about 0.3 N/mm.
- **Nest springs.** Put a thinner spring inside a thicker one. The rates add. Wind direction should be opposite so they do not tangle.
- **Pick the stiffest spring in the bag.** Thicker wire (0.6 to 0.8 mm) beats thin wire by a large factor, because rate goes with wire diameter to the fourth power. Heavy valve springs from retractable pens or lighter springs are usually the best candidates.

Measure rather than guess. Press the plunger onto a kitchen scale with the spring in a cap and read grams at 1 mm and 3 mm of travel. Aim for roughly 300 to 800 gf (3 to 8 N) at full travel for a firm detent. If the best spring gives less, make the notch ramps steeper (60 degrees from the face instead of 45) to raise the click feel without more spring force. Steeper ramps hold harder.

## Retention: why it cannot fall out

- **Front:** the shoulder (6.0 body) sits against the lip (4.6 hole). The spring force pushes the shoulder into the lip, so the plunger can never exit the front.
- **Rear:** the rear plug closes the bore. Three options, in order of recommendation:
  1. **Plug with a filament pin.** The plug is a 6.4 mm diameter cylinder, 5 mm long, that slides into a counterbore. A 1.75 mm filament offcut goes through a 1.9 mm cross hole in the housing and plug. Trim the pin flush or melt a small head on one end. This needs no hardware, and you can drive the pin out to service the part.
  2. **Screw-in plug.** M10 x 1.5 style thread, printed with 0.3 mm radial clearance. Works, but printed threads strip if over-tightened.
  3. **Snap plug.** A ring bump 0.3 mm tall into a groove. Easiest to print, but the spring force pushes on it constantly, and PETG creeps, so it may slowly walk out. Use this only if you also add a pin.
- The spring preload (1 mm) keeps the plug under a small constant load, so the pin or thread cannot rattle.

## Print orientation and settings

- **Housing:** axis vertical, lip end on the bed (open end up). The round bore prints round. The step from lip hole to bore is a 45 degree chamfer, so it needs no supports. If the fixture geometry forces the bore to lie horizontal, make the bore a teardrop (point up) and run a cleanup reamer or a 6.4 mm drill bit through it.
- **Plunger:** dome up, spring-pocket face on the bed. The pocket opens to the bed, so it needs no supports, and the shoulder under the dome is a chamfer. Layers run across the plunger axis, so the dome is layered, not stranded, and the side load on the dome acts across layer lines. If the tip wears, replace it with a 4 mm steel ball in a pressed pocket.
- **Settings:** 0.2 mm layers, 4 perimeters, 40 percent or higher infill, no ironing. Outer wall speed at 40 mm/s or less for dimensional accuracy. Slow, cool outer walls matter for sliding fits: PETG sticks to itself, so keep the sliding surfaces smooth and rub them with a dry PTFE or silicone grease.
- Use a 0.1 to 0.15 mm larger bore on the first try if your printer shows elephant foot, then adjust.

## Printing a test coupon first

Before committing the whole fixture, print a 20 mm long housing coupon with one plunger and the plug. It takes 10 minutes. Check three things:

1. The plunger slides freely under its own weight when you tilt the coupon, with no binding and no more than a visible wobble.
2. The spring force on the scale meets your target at 3 mm.
3. The plunger cannot be pulled out from the front with pliers, and the pin or plug holds when you push the plunger in hard.

If the plunger binds, add 0.05 mm to the bore diameter. If it wobbles, take 0.05 mm off the bore.

## Detent notch on the knob

Make the notches on the knob 1.5 mm deep with 45 to 60 degree ramps and a 2 mm radius bottom, so the dome seats without catching at the edges. The tip at 2.0 mm protrusion then clears the notch bottom by 0.5 mm, so the plunger rides the ramps rather than bottoming out.

## Summary

The plunger is captured by a 6.0 mm shoulder behind a 4.6 mm lip, the spring is guided in a pocket and preloaded 1 mm, and a rear plug pinned with 1.75 mm filament closes the back. Pen springs are weak, so shorten them, nest them, or pick the stiffest one, and verify the force with a kitchen scale before printing the full fixture.
