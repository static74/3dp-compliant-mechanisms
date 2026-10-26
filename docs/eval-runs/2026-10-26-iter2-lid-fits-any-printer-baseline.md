# Redesigning the 60x40 mm snap lid so one file works on any printer

## Why the lid fails today

Your lid probably relies on an interference fit, where friction between two surfaces that are a few tenths of a millimetre apart holds the lid on. Printers disagree by about 0.1 to 0.3 mm on exactly that gap. Material shrinkage, nozzle width, extrusion calibration and slicer compensation all shift it. PLA is stiff and PETG is slippery, so the same gap grips differently in each. The fix is to stop depending on the gap.

The new lid separates two jobs:

1. **Location** is done by a loose lip. It has generous clearance, so it never binds on any printer.
2. **Retention** is done by flexing hooks that engage a window in the box wall. The hook overlap (0.8 mm) is much larger than the printer-to-printer error (about 0.15 mm), so the error becomes a small fraction of the engagement.

## Dimensions to model

Assumptions: the box is 60 x 40 mm outside, with 2.0 mm walls and a 56 x 36 mm inner opening. Adjust if yours differ. All values are nominal CAD sizes. Do not scale the model or add per-printer offsets.

**Lid plate**
- 60 x 40 x 2.0 mm, sitting on the wall rim. Use 1 mm corner radii or a 0.6 mm chamfer on the underside edges.

**Locating lip (skirt) under the plate**
- Outer size 55.4 x 35.4 mm. That is 0.3 mm of clearance per side against the 56 x 36 mm opening.
- Wall thickness 1.2 mm (three perimeters at 0.4 mm).
- Height 4.0 mm.
- Add a 0.4 x 0.4 mm chamfer on the lead-in edge at the bottom.
- The lip is loose on purpose. Its only job is to centre the lid and stop it sliding sideways.

**Snap hooks: two on each long side (4 total), 8 mm wide each, centred about 15 mm either side of the lid centre**
- Hook protrusion: 0.8 mm outward from the lip face.
- Hook height: 1.5 mm.
- Lead-in ramp: 30 degrees from the insertion direction (ramp length about 1.4 mm). The ramp makes it easy to close.
- Retaining face: 60 degrees from the insertion direction. A lid you can pry off with a thumbnail and a hard stop that does not slip are both fine at this angle. Use 90 degrees if you never want it opened again.
- Free beam length (the flexing part): 14 mm.
- Beam thickness (the flexing direction): 1.2 mm.
- Relief slots: cut through the lid plate on each side of the beam, 1.0 mm wide and 16 mm long. Without them the plate holds the beam rigid. The plate then cannot flex at the root.
- Check the strain: strain = 1.5 x thickness x deflection / length squared = 1.5 x 1.2 x 0.8 / 14^2, which is about 0.9 percent. That is safe for PLA (limit about 2 percent) and comfortably safe for PETG (4 percent or more).

**Box side**
- Cut a rectangular window through each long wall at each hook location: 9 mm wide (8 mm hook plus 0.5 mm per side) and 2.0 mm tall (1.5 mm hook plus 0.5 mm slack).
- Place the window so its upper edge sits 4.0 mm below the rim, which is where the hook retaining face lands when the lid is fully seated. Check this against your hook height in the model before printing.
- The lid also rests on the rim, so the window's upper edge only has to stop it lifting. Leave the lid free to settle.

## Why this works on both printers

- The 0.3 mm lip clearance absorbs a 0.15 mm error either way and never goes below 0.15 mm.
- The hooks overlap 0.8 mm. A 0.15 mm change in wall thickness is under 20 percent of that engagement, so the lid neither falls off nor needs a hammer.
- The beam is long and thin, so the closing force stays low in stiff PLA. In slippery PETG the retaining face still catches because the engagement is positive and mechanical, not friction.
- Open windows let you see the hook seated, which gives you a visual check.

## Print orientation

**Lid:** print flat with the outer (top) face on the bed and the lip pointing up. Because the beams are cut in the plane of the plate, they bend sideways in the XY plane. Their layers then run along the beam's length, so bending stress runs along the layers, not across layer bonds. This is the strong direction. Do not print the lid lip-down with the beams standing vertically. Their bending stress would then pull layers apart, and they would snap on the first close.

**Box:** print open side up, so the windows are vertical holes. A 9 x 2 mm window prints fine without supports because its roof is only 9 mm wide. If it sags on your printer, make the window top a 45 degree chamfered peak instead.

**Slicer settings (same for both printers)**
- 0.2 mm layers, 0.4 mm nozzle, 3 or more perimeters, 100 percent line width is fine.
- Turn on first-layer or elephant-foot compensation (about 0.1 to 0.15 mm) in the slicer, not in CAD.
- No supports.

## Validation

Print a test coupon before the full part: one lid-lip corner and one 20 mm length of box wall, including one hook and one window. It prints in a few minutes. Have your coworker print the same coupon on his Bambu in PETG. If it closes with a firm click on both machines, release the full design.

## If the coworker's print still feels loose or tight

Change one number only, the hook protrusion, in 0.1 mm steps (0.7 to 1.0 mm). Do not change lip clearance. That keeps one master file with one tuning knob.
