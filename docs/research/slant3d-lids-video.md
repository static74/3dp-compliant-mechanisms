# Video 1 report: Slant 3D, "Design Compliant Lids for Perfect Tolerance Every Time"

Source: https://www.youtube.com/watch?v=IZKh6lo9SP4
Title: "Design Compliant Lids for Perfect Tolerance Every Time | Design for 3D Printing: Lids: Vol. 2"
Creator/uploader: Slant 3D (on-camera presenter wears Slant branded jacket; name not stated). Duration 6:17 (377 s), 1280x720.
Evidence: YouTube auto-captions (en) plus 56 scene-change frames plus ~100 full-resolution frames pulled around the CAD and slicer segments. Frames and hi-res crops are in video1/ (frames/ under watch-423pfp4a/, hi/, z_*.jpg).
Label convention: STATED = spoken or readable on screen. ESTIMATED = my inference from frames, or arithmetic from an on-screen readout.

## 1. Framing
- Question the video answers (0:00-0:12): how to make a lid fit its box "perfectly every single time without having to worry about any of the slicer settings."
- Thesis (0:14-0:44, 5:20-5:45): fit varies with filament colour (shrinkage), machine, settings, infill, nozzle size, resolution, and material (PETG vs PLA, white vs black). Do not rely on tuned clearances. Make the geometry itself tolerant by using compliance (flex), reduced contact area, and built-in latches.
- Progression: (A) basic press-fit lid with rounded edges and first-layer chamfer, (B) lid with perimeter cut-out holes to reduce contact, (C) in-plane side springs, (D) grip fins, (E) internal spring latches with detents.
- The video is a conceptual overview with a CAD demo. It gives very few numbers. Every dimension below that is not marked STATED is inferred.
- Closing plug (5:54-6:10): Slant 3D "Teleport" app, where you upload files and Slant prints and ships them to your customers. Designing for tolerance-independence matters when others print your files or when you scale production. No URL or file download is given in the audio or frames.

## 2. Common test part (all mechanisms share it)
- Open-top box ("yellow box") plus a lid with a flange and an inserted plug. Lid is a two-step stack: a wide flat flange plate on the bottom and a smaller plug that drops into the box opening.
- Base box/flange footprint: 85 mm x 85 mm (STATED on screen, Shapr3D dimension callouts "85 mm" on both edges of the first extruded face at ~0:45). I first misread this as 65 at low resolution; the 1280-px crop clearly reads 85.
- Plug footprint: ESTIMATED 75 x 75 mm. Derivation: Shapr3D shows a selection readout of "8 edges 291.4159 mm" and "8 edges 331.4159 mm" (0:51-0:54). A rounded square of side s and corner radius r has perimeter 4s - 8r + 2*pi*r. With r = 5 mm, s = 75 gives 291.4159 and s = 85 gives 331.4159. Both match exactly, so the flange is 85 mm with 5 mm corner radius and the plug is 75 mm with 5 mm corner radius (ESTIMATED, derived). That implies a 5 mm step on each side between flange and plug. The box wall thickness and plug-to-wall clearance are not shown.
- Heights: not stated. By eye the flange is ~3 mm thick, the plug ~6-8 mm, the box ~25-30 mm tall (ESTIMATED from hand-held frames).
- Lid appears printed flat, flange face down on the bed (layer lines parallel to lid plane; side springs are "in plane," see below). Slicer preview at 2:18 and 2:20 shows the flange on the bed with the plug above it.
- Colours are only for show: orange = plain press-fit, pink = perforated-edge lid, yellow = side-spring lid, purple = grip-fin lid, white = latch lid.

## 3. Mechanism A: Standard press-fit lid (baseline)
Timestamps: 0:45-0:58 (talk) ; CAD 0:45-0:58 ; hands 1:07-1:16.
- Purpose: "a standard lid that's just going to be pressed into another thing." Presented as the simple, not-necessarily-right baseline.
- Rules STATED: round all edges; chamfer the very first layer to avoid elephant footing; then it "will generally fit fairly true."
- Problem STATED (1:07-1:14): lots of contact on the outer walls, so any deviation fights a large surface area.
- Geometry: flange 85 mm square; plug ~75 mm (derived). Chamfer size and fillet radius: NOT STATED. The tool readout in CAD shows only perimeter sums. Chamfer is applied to the bottom edge of both the flange and the plug (Chamfer/Fillet tool, 8 edges selected, 0:49-0:55). Outer vertical corners filleted, radius 5 mm (derived above).
- Material/print: not stated.
- CAD steps as shown (Shapr3D on iPad with Apple Pencil, ESTIMATED from UI):
  1. Sketch an 85 x 85 mm square on the top plane, extrude one-sided to make the flange (0:45).
  2. Sketch/offset a smaller square on the flange top, extrude to make the plug.
  3. Fillet the four vertical corner edges (r = 5 mm, derived).
  4. Select the 8-edge bottom loops (flange and plug) and apply Chamfer for first-layer/elephant-foot relief (0:49-0:55).
- Use/lock: friction fit only. Solid versions are permanent: "if you want it to be permanent, go ahead and go with a solid version" (1:45).

## 4. Mechanism B: Perforated-wall (reduced contact) plug
Timestamps: 1:16-1:47 (CAD 1:16-1:27; hands 1:28-1:45).
- Purpose: reduce surface contact on the plug so it inserts easily and layer lines do not interlock, "so you can make a tighter fit but still have it kind of loose" (1:30-1:35).
- Variants STATED: cut holes around the outer wall; or go all the way to "a single nubbing" so only a couple of points touch the walls and the lid is easy to open (1:36-1:43). Solid version for permanent.
- Geometry as shown (pink lid, frame at 1:28 and CAD at 1:16-1:26): scalloped plug edge made by cutting semicircular/cylindrical pockets into the plug perimeter. About 5 pockets per side visible on the pink sample; CAD shows roughly 5 circles across one edge, then a pattern repeated around the perimeter, ~20 cylinders total with "60 faces" selected (ESTIMATED). Circle diameter not stated; estimated ~8-10 mm relative to the 75 mm plug. Pocket depth into the wall: not stated.
- CAD procedure as shown (ESTIMATED from the Shapr3D toolbar labels "Circle", "Linear Pattern", "Circular Pattern", "Extrude One-Sided"):
  1. Start a sketch on the plug top face (top view showing flange, plug outline and fillets).
  2. Draw one circle centred on the plug edge.
  3. Linear Pattern the circle along one edge (5 copies visible).
  4. Circular Pattern (4 copies at 90 degrees) to repeat around the square (visible at 1:24-1:26).
  5. Extrude (cut) the circles down through the plug wall height. Result: cylinder-shaped scallops, with the cut faces highlighted cyan at ~1:26.
- Print specifics, material, failure modes: not stated.

## 5. Mechanism C: Side springs ("simple compliant mechanisms ... side springs")
Timestamps: 2:00-2:55 (talk); CAD 2:03-2:12, 2:26-2:50; slicer 2:18-2:21; hands 2:03, 2:21, 2:32, 2:39-2:50.
- Purpose: universal lid fit. Spring arms flex sideways into the box wall, absorbing dimensional error from any printer/material.
- Key design rule STATED (2:08-2:25): do NOT build springs vertical across layer lines; they "can push out and snap along the layer lines." Instead make the springs "right in plane of the part," i.e., the arm is a thin cantilever cut out of the plug wall, whose long axis and flex direction lie in the XY (layer) plane, so layers run along the arm. This gives "as much flexibility as you could possibly want while still having good rigidity."
- Tuning STATED: thicken the outer arms for a tighter fit, thin them for a loose nice fit (2:26-2:35). Add small nubs on the arms that press into the wall or into a dot/dimple in the box (2:35-2:43). Result: "really nice action, very easy fit ... really low tolerance part."
- Geometry:
  - Two arms on the sample, both on the same wall, with a solid post between them (yellow lid, 2:03 and 2:32: two horizontal slots near the top edge of the flange).
  - Slot/arm sketch: a rectangle drawn along the plug wall; the on-screen dimension reads "25 mm" when first placed (2:07) and settles at 22.5074 mm (readout "22.5074 mm", hence an arm roughly 22.5 mm long) with a second dimension ~2.5 mm (partially legible) for wall/slot width (2:07-2:08). Treat 22.5 mm x ~2.5 mm as ESTIMATED (hand-sketched, the creator does not state them).
  - Fillet on the arm tip/slot corners: on-screen label "R1 mm" at 2:27 (STATED on screen: 1 mm radius). Chamfer/Fillet tool used again at 2:29-2:31 to round outer arm corners.
  - Nub on each arm: small round nub (diameter roughly 2 mm, protruding ~0.5-1 mm; ESTIMATED from frames at 2:36-2:50, nubs seen at the free end of each arm; Shapr3D shows a small circular extrude on the outer face).
  - Bottom relief: the arms are separated from the flange by a gap under the arm so they can move (visible as dark-blue overhang line under each arm in the slicer preview at 2:20).
  - Gap value between arm bottom and part bottom: spoken as "a .3 space" (3:39-3:44, in the fin section but applied to the same cut-out technique). On-screen Shapr3D shows 0.2 mm (see section 6). Conflict noted.
- Print specifics: slicer preview at 2:18-2:21 (PrusaSlicer-style colour scheme, ESTIMATED) shows lid printed flange-down, with the gap beneath each arm bridging as an overhang perimeter. No layer height/infill/wall numbers given. Avoiding slicer tuning is the point of the video.
- CAD steps as demonstrated (Shapr3D, ESTIMATED):
  1. On the plug top face, sketch a rectangle (Rectangle: Diagonal) along one wall, about 22.5 x 2.5 mm; mirror/pattern for the second arm (2:03-2:12).
  2. Extrude-cut downward to form the slot behind each arm, so the arm is a free cantilever attached to the wall at one end and the post.
  3. Chamfer/Fillet the arm edges at R1 mm (2:26-2:31).
  4. Select the arm outer face, extrude a small circular boss for the nub (2:36-2:50; "2 faces" selected, offset readout ~0 mm and 32-36 mm distances shown in the bottom bar).
  5. Cut the relief below the arm (extrude one-sided to remove material under the free end; see 0.2 mm gap).
- Use: lid presses into box; arms deflect inward over the box rim and spring back; nub seats in a dot/dimple or presses into the wall.
- Failure modes STATED: arms perpendicular to layer lines snap; one arm can break off (2:58-3:00, motivating fins).

## 6. Mechanism D: Grip fins
Timestamps: 2:55-3:45 (talk); CAD 3:03-3:12 (line sketch) and 3:20-3:42; hands 3:12-3:30, 3:56, 4:00; slicer 4:19.
- Purpose: tighter fit and redundancy compared with two side springs. "You just take that little flange and take it all the way around," making the outer walls of the plug slightly larger than the opening (2:58-3:11). Compliance remains so the lid is removable, "as opposed to ... pry it back out" (3:16-3:21).
- Tuning STATED (3:23-3:30): longer fins = softer touch; thicker/thinner fins as with any spring.
- Geometry:
  - Fins run around all four sides of the plug (purple lid, 3:12 and 3:28). Roughly 25-30 fins per side (ESTIMATED by counting at 3:56, count approximate), each a thin slanted blade (slanted ~45 degrees in the top-view slicer capture at 4:19 and in the sketch at 3:47-3:56; angle ESTIMATED 45 +/- 10 degrees from the sketch lines).
  - Fin pitch and thickness: not stated; ESTIMATED ~0.8-1.2 mm thickness and ~2 mm pitch from the 75 mm plug and fin count.
  - Fin height: runs most of the plug height, ending 0.2 mm above the flange (see next bullet).
  - Interference: the finned perimeter is deliberately larger than the box opening; amount not stated.
  - Bottom relief: STATED gap "a .3 space between the bottom of the fin and the bottom of the part so that they can break loose" (3:39-3:44). On-screen Shapr3D extrude readout at 3:32-3:38 shows "0.2 mm" (dimension label "0.2 mm", bottom bar "dZ: 0.2"), a 90 degree angle label, and a 9.3973 mm length. So the spoken value (0.3) and the screen value (0.2) disagree; the drawn model uses 0.2. I recommend treating this as 0.2-0.3 mm.
  - A small bevel/radius sits at the top of each fin edge (rounded top lead-in) and the corners have a solid 90 degree corner block (rounded) with no fins (3:12 frame; corners left solid).
- CAD procedure (ESTIMATED from Shapr3D toolbar labels, Line/Arc, Linear Pattern, Extrude, Pattern, Chamfer/Fillet):
  1. Sketch one slanted line/thin parallelogram on the plug top face along one edge (3:03-3:12, 'Sketch 07').
  2. Linear Pattern it along the edge (dense blue hatch visible at 3:12-3:17, then at 3:20 the whole perimeter is hatched on all four sides with corners skipped).
  3. Extrude-cut the hatch down through the plug wall to form slots; remaining ribs are the fins (3:23-3:28, "Extrude One-Sided", highlighted in cyan).
  4. Extrude a 0.2 mm slab/cut at the base (3:32-3:42) so the fins hang free of the flange; this is the relief gap.
  5. Optionally fillet the top of the fins.
- Print: the slicer top view at 4:19 shows the fin lid with slanted diagonal strokes along the perimeter and diagonal solid fill on the lid face (ESTIMATED: flange-down orientation, fins printed as vertical blades whose full outline lies in each layer, so they flex in-plane). Layer height/walls/infill not stated.
- Use: lid pushes into the box; fins bend over the rim and "grip." A craft-knife demo at 3:44-3:47 shows trimming/clearing the corner of the fin set (ESTIMATED purpose: removing stringing or first-layer flash at the corner).
- Failure mode: stuck fins if the 0.2-0.3 mm bottom gap is omitted.

## 7. Mechanism E: Internal spring latches with detents
Timestamps: 3:48-5:20 (talk); hands 4:50-5:16; hook-tool demo 4:55; cross-section render 5:58-6:03.
- Purpose: more travel than any fin can give: "almost 2 mm of distance that they can travel in order to create a latch" (4:54-4:59, STATED). The lid contains "literally internal springs, internal latches," printed in place. Small latches at the front end are pushed in and out by a spring inside the lid (4:20-4:36).
- Design notes STATED: it is harder than fins; "you have to really mess with the design of it to make sure that it's robust" (4:39-4:42). Hang/bridge above the latch can make the latch jam inside, so the roof over the latch cavity must be designed to print without drooping (4:45-4:49).
- Matching features STATED: detents in the box so the latches have somewhere to go, and "little channels" (5:06-5:10). Tuning the latch gives a good fit "all the way around."
- Geometry: ~2 mm travel (STATED). All other dimensions not given. Visual (white lid, 4:50-5:16): a small rectangular latch nub, ~5 mm wide x ~2-3 mm tall (ESTIMATED), sits in a slot in the plug wall; a hooked tool (4:55) pulls it back to release. A render at 5:58 (dark background) shows a C-shaped clip cross-section: a rigid back wall with a long curved cantilever arm on the left (spring) and two hook lips at the top and bottom of the C. The arm has an S-curve and tapers; this appears to be an illustrative clip, not a specified part (ESTIMATED).
- CAD/print procedure: not demonstrated. No slicer settings or clearances shown.
- Use: lid snaps into box; latch retracts under the spring when pressed against the wall, then extends into the detent. Release with a tool or fingernail on the latch face (hook tool in the 4:55 frame).

## 8. Material and process notes (all mechanisms)
- PLA/PETG: STATED only as examples of why clearance-tuned fits break "as you move from PETG to PLA or from white to black or from this machine to that machine" (5:23-5:30). No material recommendation per mechanism. No TPU mention. No layer height, perimeter count, infill percentage, supports, or print-in-place clearance are stated anywhere.
- Printers shown: Slant's printer farm at 5:31 (B-roll). Not the demo parts' printer.
- Slicer: preview looks like PrusaSlicer's colour-by-feature view (ESTIMATED), used only to show geometry (spring arm gap overhang and slanted fin infill).

## 9. Software
- CAD: Shapr3D on an iPad with Apple Pencil (ESTIMATED from the UI: "Modeling / Items" tabs, "Extrude - One-Sided", "Chamfer/Fillet", "Pattern: Linear/Circular", "Constraint Settings" panel). Project name on screen "untitled project".
- Slicer preview: PrusaSlicer-style (ESTIMATED).

## 10. Timestamp index
| Time | Item |
|---|---|
| 0:00-0:12 | Hook and promise |
| 0:14-0:44 | Why tolerance is hard; robust-design thesis |
| 0:45-0:58 | Standard lid; round edges; first-layer chamfer; CAD (85 mm square, chamfer on 8-edge loops) |
| 1:01-1:16 | Why solid lids fail: too much outer wall contact |
| 1:16-1:47 | Perforated plug, single-nub variant, permanent solid; CAD circle pattern |
| 1:48-2:02 | Solid versions are not compliant; introduce side springs |
| 2:03-2:55 | Side springs: in-plane rule, thickness, nubs; CAD rectangle 22.5 mm, R1 mm fillet, nub extrude; slicer view |
| 2:55-3:45 | Grip fins; CAD slanted-line pattern; 0.2 mm bottom gap (spoken .3) |
| 3:48-5:20 | Internal spring latches, 2 mm travel, jam warning, detents |
| 5:20-5:50 | Summary: tolerance-independent design |
| 5:51-6:10 | Teleport plug; sign-off |

## 11. Referenced files, links, promises
- No downloadable files, STEP/STL names, or URLs are stated or shown. The description page was not scraped (the skill only fetched metadata and captions). "Vol. 2" in the title implies a series (Lids), but earlier/later volumes are not named.
- Promised but not delivered: "finish off with designing some compliant mechanisms" (0:12) is delivered only as a fast CAD time-lapse with no narration of dimensions; the latch section is described but not modelled on screen.

## GAPS (parameters needed to reproduce that the video did NOT give)
General
- Layer height, nozzle diameter, perimeter count, top/bottom layers, infill type and percentage, speed, cooling, supports, build orientation confirmation, material per mechanism, shrinkage compensation, and the printer used for the demo parts.
- Box dimensions: wall thickness, interior depth, total height, corner radius of the opening (only the 85 x 85 mm outer footprint and a derived 75 x 75 mm plug at 5 mm corner radius are known). Flange thickness, plug height.
- Plug-to-opening nominal clearance (the whole point of the video is that it should not matter, but the nominal numbers for the demo parts are not given).
- Chamfer size on the first layer and fillet radius on lid edges (only R1 mm on spring-arm corners appears).
Mechanism B (perforated plug)
- Hole/scallop diameter, depth, spacing, count per side, whether holes are through the plug wall or blind.
Mechanism C (side springs)
- Arm length, thickness, width and root fillet (22.5 mm and about 2.5 mm are estimates from a half-legible sketch label); slot width behind the arm; deflection distance; nub diameter and height; mating dimple dimensions in the box; whether arms are on one side or all four sides (sample shows one wall with two arms).
Mechanism D (grip fins)
- Fin count, thickness, pitch, slant angle (estimated 45 degrees), fin length, interference with the box opening, height, top lead-in shape, corner treatment dimensions. Spoken 0.3 mm vs on-screen 0.2 mm bottom gap is unresolved.
Mechanism E (latches)
- Everything except "almost 2 mm of travel": spring type and geometry (leaf, S-curve, coil-like), spring thickness and length, latch size and ramp angle, hook depth, detent depth and shape, channel dimensions, cavity roof design to avoid droop (e.g., teardrop/chamfer angle), clearance around the moving latch, support strategy, material. No CAD walkthrough is shown.
- Release mechanism geometry (the hook-tool access slot size).

---

# MEASUREMENTS (follow-up pass)

All frames below are full-resolution (1280x720) PNG extractions in video1/m/ . Method: calibrate pixels per mm from a feature of known size in the same frame (85 mm flange, 75 mm plug, 5 mm corner radius, or a Shapr3D dimension label), then measure on zoomed crops. "Derived" means computed from a Shapr3D selection readout, which is more precise than any pixel measurement. Time = seconds into video. Where a frame is oblique, I note the foreshortening correction.

## Corrections to the earlier report (found in this pass)
1. CAD software confirmed as Shapr3D. The video description's "Try Our CAD Software (Use Code "Slant3d" for 10% OFF)" tinyurl redirects to shapr3d.com/download (utm_campaign=slant3d_affiliate). A "Details in Description" banner is on screen at about 0:54. The description lists no model files. Its other links: Teleport tinyurl (redirects to slantpod.com, a Slant POD page), a "$10 Filament" tinyurl, and two other channels (Slant POD, Tangled). The description says the video is "Produced by Geometry Media".
2. The "C-shaped clip" render at 5:58-6:03 is NOT a latch or spring study. Frames at 358-363 s (m/cc_sheet.jpg, m/clz.png) show it is a sample Teleport product: a white belt/phone-style clip that turns blue with a "BUY NOW" button, then a black Slant-branded clip being unboxed. Disregard my earlier reading of it as spring geometry. Proportions anyway: overall height about 2 x its width (about 195 x 380 px at 1024 scale in frame_0054.jpg), back spine about 7 percent of the width, a single long tapered cantilever arm on the back side, and two inward hook lips at top and bottom.
3. The latch lid has latches on TWO opposite walls (m/la_292.png at 292 s shows a window on the left wall and on the right wall). Earlier text implied one.
4. The slicer close-up at 4:48-4:49 (m/lt_288.png) is the latch window, not the side-spring lid (see Latches below).
5. Heights: the earlier "flange ~3 mm" was too thin. Measured flange is about 6 mm, plug about 8 mm (see section 5 below).

## 1. Grip fins
Calibration: m/lp_184.png / m/lpz_all.png (184 s, zoomed Shapr3D sketch 07): the slit width label reads "0.5 mm" (on screen), and its two top endpoints are 30 px apart in the 4x crop, giving about 60 px per mm in the 4x zoom (about 15 px/mm in the source). Cross-check: the plug outer corner arc has radius about 300 zoomed px = 5.0 mm. Agreement within 5 percent.

| Quantity | Value | Method / frame | Range |
|---|---|---|---|
| Slit (cut) horizontal width | 0.5 mm | STATED on screen, m/lp_184.png ("0.5 mm" label) | exact |
| Slit shape | thin parallelogram (4 edges), slanted | m/lpz_all.png | |
| Slit length along its axis | 7.19 mm | Derived: selection readout "140 edges, 538.1237 mm" (m/tv_188.png, 188 s). 140 edges / 4 edges per slit = 35 slits; 538.1237 / 35 = 15.375 mm perimeter each; (15.375 - 2 x 0.5) / 2 = 7.19 mm | +/-0.05 |
| Slit length, pixel check | 7.20 mm | m/lp_184.png: dx 3.0 mm, dy 6.55 mm | +/-0.3 |
| Slit angle from wall normal | 24.6 deg (so about 65 deg to the wall) | atan(3.0 / 6.55), m/lp_184.png | +/-3 deg |
| Slit depth into plug (normal to wall) | about 5.0 mm inside the outer wall, plus about 1.55 mm of the sketch sticking out past the wall | same frame, wall edge at y = 1060 zoomed px | +/-0.3 |
| Slits per side | 35 | Derived from 140 edges (above); visual count in m/tv_187.png (h1.png + h2.png) gave about 33-34 visible, with the pattern ends faint | 33-35 |
| Fins (ribs) per side | 36 | one more than slits; photo count in m/pf_236.png / pfa.png / pfb.png gives 36-37 | 35-37 |
| Pitch along the wall | 1.9 mm | m/tv_187.png: 8.8 px spacing / 4.706 px/mm (flange 400 px = 85 mm); also 65 mm straight run / 34 gaps = 1.91 | +/-0.1 |
| Fin thickness (horizontal) | 1.4 mm (pitch minus 0.5) | arithmetic | +/-0.15 |
| Fin thickness (perpendicular to slit) | 1.27 mm | 1.4 x cos(24.6 deg) | +/-0.15 |
| Straight run of fins per side | about 64.6 mm | 34 x 1.9; matches 75 - 2 x 5 = 65 | +/-1 |
| Bottom relief under fins | 0.2 mm | STATED on screen, m/gb_all.png and video1/z_t200_13.jpg, readout "0.2 mm" and "dZ 0.2" at 3:32-3:38 (spoken ".3") | exact on screen |
| Fin height (free, excluding the 0.2 gap) | about 7 mm | m/pf_236.png: 34 px / (cos 26 deg x 5.35 px/mm) | +/-1.5 |
| Interference (fin tips standing proud of the plug wall) | not measurable; fin outer faces appear flush with the solid corner blocks | m/pf_236.png, pfb.png | 0 +/-0.5 mm |
| Corner treatment | corners left solid (about 5 mm of R5 corner with no slits at each end); slits stop where the corner arc starts | m/tv_188.png, pfb.png | |
| Fin top | rounded top edge (fillet, size not resolvable, about 0.5-1 mm) | pfa.png | |

Shapr3D readouts zoomed (as requested):
- 3:03-3:12 (182-192 s): "0.5 mm" (slit width, 184 s); "Sketch 07" tab; status bar "140 edges 538.1237 mm" (187-188 s); tool names Line/Arc, Linear Pattern then Circular Pattern (4 copies at 90 deg for the other three walls).
- 3:32-3:38 (212-218 s) bottom bar (m/gb_all.png): "angle 90 deg | 9.3973 mm | dX 7.1496 | dY 6.0985 | dZ 0.2". Check: sqrt(7.1496^2 + 6.0985^2 + 0.2^2) = 9.399 mm, so the bar shows a vector between two snap points whose Z component is 0.2 mm. Label above the extrude handle: "0.2 mm". (The dX 7.15 is close to the slit length 7.19.)
- The extrude at 3:23-3:28 shows "82 faces" selected (m/tv_189.png, bar reads "82 faces").

## 2. Perforated plug
Calibration: m/h_83.png (83 s, top view): flange 276 px = 85 mm, so 3.247 px/mm (plug 243 px = 74.8 mm, consistent). Zoom m/h83z1.png (10x): 32.5 px/mm.

| Quantity | Value | Method | Range |
|---|---|---|---|
| Hole diameter | 10.0 mm | Derived: readout "5 edges 157.0796 mm" (m/h_83.png) = 5 x pi x 10; pixel check 338 px / 32.5 = 10.4 | exact (derived), pixel +/-0.5 |
| Holes per side | 5 | m/h_83.png | exact |
| Total holes | 20 (5 on each of 4 sides, none at the corners) | Circular Pattern, m/h_83.png | |
| Pitch (centre to centre) | 13.5 mm | m/h83z1.png: 440 px / 32.5 = 13.55; m/h_83.png 43.75 px / 3.247 = 13.5 | +/-0.3 |
| Wall land between holes | about 3.5 mm | 13.5 - 10 | +/-0.3 |
| Row length | about 64 mm (4 x 13.5 + 10) | arithmetic | |
| Offset of first hole from the corner | about 5.5 mm | (75 - 64) / 2 | +/-0.5 |
| Hole centre position | about 2.0 mm inside the plug outer wall (circle runs 3.2 mm outside the wall and 7.2 mm into the plug) | m/h83z1.png: centre x = 290 vs wall x = 225 | +/-0.3 |
| Pocket depth into the plug, perpendicular to the wall | about 7.2 mm; opening width at the wall about 9.2 mm | geometry of a 10 mm circle centred 2 mm inside | +/-0.5 |
| Through or blind | cut down the full plug height and stop at the flange top (blind to the flange, not through it) | ESTIMATED: cyan pocket floors at the base in the 3D view around 84-86 s; arched pockets in the pink photo | not measured |

The earlier "diameter 8-10 mm, about 20 cylinders" estimate is now confirmed as 10.0 mm and 20 holes.

## 3. Side springs
Calibration: m/sp_128.png (128 s): the rectangle width reads "22.5074 mm" on screen over 272 px, so 12.1 px/mm; cross-check with the outer rectangle "25 mm" over 302 px = 12.1 px/mm.

| Quantity | Value | Method / frame | Range |
|---|---|---|---|
| Slot footprint rectangle (outer) | 25 mm x 5 mm | STATED on screen at 127 s: "25 mm" and vertical label "5 mm" (m/spz_all.png, video1/z_dim_127.jpg) | exact |
| Edited inner rectangle | 22.5074 mm long x 2.5 mm | STATED on screen at 128 s: "22.5074 mm" and vertical label "2.5" (m/spz_all.png right tile). I could not read the second label at 2:07 before; it is the vertical height, first "5 mm" and then changed to "2.5" | exact |
| Arm length | 22.5 mm | the 22.5074 label | +/-0.1 |
| Arm thickness | 2.5 mm | inner rectangle height; pixel check 29 px / 12.1 = 2.4 | +/-0.2 |
| Slot width behind the arm | 2.5 mm (the other half of the 5 mm footprint) | 59 px - 29 px = 30 px / 12.1 | +/-0.3 |
| Free-end gap beside the arm | 2.5 mm at the left end (arm joins the wall at the right end of the sketch, so it is a cantilever) | sp_128.png: outer rectangle starts 30 px left of the inner one | +/-0.3 |
| Number of arms | 2 | m/nb_159.png (159 s, finished CAD, left view) | exact |
| Walls | one wall only (the far wall in the view); the other three walls plain | m/nb_159.png; yellow photo at 2:32 shows two slots on one edge | |
| Arm spacing | gap between the two arms about 14.6 mm; slots about 25.5 mm and 25.2 mm long; total span about 65 mm, centred (about 10 mm from each flange edge as seen through the flange) | frame_0027.jpg (2:32): 105 px slot, 60 px gap on a 350 px = 85 mm flange (4.12 px/mm) | +/-1 |
| Arm corner fillet | R1 mm (STATED on screen at 147 s, label "R1 mm") on the vertical arm edges | video1/z_chs.jpg | exact |
| Nub diameter | about 1.6 mm (up to 2 mm) | m/nb_159.png: 16 px dot on a 226 px arm = 22.5 mm | +/-0.5 |
| Nub position | on the outer face, about 75 percent along each arm toward the right end, low-middle in height | nb_159.png: arm 1 74 percent, arm 2 76 percent | +/-5 percent |
| Nub protrusion | small dome, not measurable; appears 0.3-0.5 mm | | +/-0.3 |
| Arm bottom relief | 0.2 mm (same cut as the fins; spoken ".3") | | |

## 4. Latches
Calibration: m/lb_312.png (312 s, edge-on white lid): flange 475 px = 85 mm, so 5.59 px/mm (plug 422 px = 75.5 mm, consistent). View is tilted about 26 deg downward (top face depth 185 px for 75 mm gives sin = 0.44), so vertical dimensions are divided by cos(26 deg) = 0.9. Zoom: m/lb312z.png (4x).

| Quantity | Value | Method / frame | Range |
|---|---|---|---|
| Window in the plug wall (square-ish pocket around the latch) | about 7.9 mm wide x 5.4 mm tall | lb312z.png: 177 px / 4 / 5.59 = 7.9; 107 / 4 / 0.9 / 5.59 = 5.3 | +/-0.8 |
| Window per slicer close-up | about 7.6 x 6.9 mm (assuming 0.2 mm layers: 7.1 px per layer, 36 px/mm) | m/lt_288.png (288 s), layer pitch measured as 7.1 px from the raw pixel column; scale rests on the 0.2 mm assumption | +/-1.0 |
| Latch block | about 6.9 mm wide, with a thin tan gap line (about 0.3-0.5 mm) on its top, right and bottom edges | lb312z.png | +/-0.8 |
| Protrusion of the latch beyond the plug wall | flush to about 0.5 mm proud; not resolvable | lb312n.png | 0 to +0.5 |
| Horizontal position | centred on the wall (window centre x = 647 vs plug centre 651 px, offset under 1 mm) | lb_312.png | +/-1 |
| Vertical position | window bottom at or just above the flange top; top about 1-1.5 mm below the plug top edge | lb312z.png | +/-1 |
| Number | one latch window at the centre of each of two opposite walls | la_292.png | |
| Slicer close-up details (288-289 s) | square window outlined by dark-blue overhang perimeters on top and bottom edges, a cyan zig-zag bridging line just below the top edge, faint curved shadows on the left and right sides suggesting a curved sidewall of the spring cavity | lt_288.png | |
| Box detents/channels | not shown; no view into the box interior anywhere in the video | | |
| Internal spring shape | not shown in any frame; only the slicer window close-up hints at it. The C-clip render is an unrelated Teleport sample product (see corrections) | | |

## 5. Heights, box wall, chamfer
| Quantity | Value | Method / frame | Range |
|---|---|---|---|
| Box outer footprint | 85 x 85 mm | STATED (Shapr3D) | exact |
| Box height | about 26 mm | m/pk_86.png (86 s, nearly side-on, tilt under 3 deg): 188 px / (620 px / 85 mm) | +/-1.5 |
| Box wall thickness | about 5 mm at the rim, with a stepped inner ledge: derived (85 - 75) / 2 = 5 mm minus the plug clearance; rim strip measured about 4.6 mm in m/f7z.png (19.5 px/mm) | | +/-1 |
| Flange thickness | about 6 mm | m/lb_312.png (6-7 mm) and frame_0018.jpg zoom m/f18z.png (about 6.1 mm at 16.3 px/mm); slicer layer count (flange top at 220 px of 577 px lid height at 36 px/mm) gives 6.1 mm | +/-1 |
| Plug height | about 8 mm (7-10 mm across methods): lb_312: 8; pf_236: 7; slicer layer count: 10 (assumes 0.2 mm layers) | | +/-2 |
| Total lid height | about 14-16 mm | slicer close-up: 577 px / 36 px/mm = 16 mm (0.2 mm layer assumption); photos 14 | +/-2 |
| Layer height | not stated. 7.1 px per layer in lt_288.png; 0.2 mm is consistent with the designer's 0.2 mm relief gap (one layer) | | assumption |
| Chamfer on the first layer | not resolvable; visible in CAD as a thin bevel on the flange and plug bottom edges, at most about 1 mm | m/c_55.png (55 s) | <=1 mm |
| Plug top edge fillet | about 2 mm wide band along the plug top edge (visible gradient band 2.0-2.2 mm in m/h83z1.png and m/lpz_all.png) | | +/-0.3 |
| Corner radius | R5 (derived from perimeter readouts) | | exact |
| Plug-to-flange step | 5 mm per side | h83z1.png: (225 - 60) / 32.47 = 5.1 | +/-0.2 |

## Residual gaps after measurement
- Layer height, perimeters, infill, material, and the slicer used remain unstated. The 0.2 mm layer height is an inference.
- Latch spring, detent and channel geometry are never shown.
- Fin interference (how far the fin tips exceed the box opening) is not visible; the box opening size and the plug clearance are not shown.
