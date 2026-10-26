# Video report: "Ultimate Guide to Connecting 3D Printed Parts | Pins, Fins, Slots, & Snaps"

URL: https://www.youtube.com/watch?v=vsHpiHhB3RU
Creator/channel: Slant 3D (presenter unnamed on screen; produced by "Geometry Media" per description). Duration 32:29.
Evidence base: auto-captions (full), 120 scene-change frames at 1024 px, extra native-res 1280x720 frames of CAD screens, YouTube description + chapter list. No slicer settings, layer heights, or material names were stated anywhere, so there are almost no print-profile numbers to report (see GAPS).

IMPORTANT FRAMING CORRECTION: this is NOT a compliant-mechanism / print-in-place video. It is a compilation of ~5 earlier Slant 3D shorts about *separable joints between parts of a larger assembly* (pegs, slots, tongues, snap tabs, glue features). "Flexible" content = spring flanges / grip fins / locking tabs that elastically deform on press-fit. Nothing is printed assembled; every joint is printed as two parts and pressed together. The only genuinely "impossible-geometry" items are the grip-fin eye slot and the internal-recess locking tab.

Overall thesis (said at 0:14-0:20, 23:44-24:44, 31:28-32:04): design joints so they work on any machine, material, slicer and setting, with no tuned clearances ("If you're tweaking slicer settings, you're not designing a product. You are being an artisan"). The method is to replace fixed-clearance fits with features that self-center, wedge, or elastically flex, and to orient/chamfer so no supports are needed.

Software shown:
- Shapr3D on iPad with Apple Pencil: diamond peg, slab, S-bracket, C-clamp, horizontal pin tutorial b-roll, all vertical pin/cross pin/fluted pin demos (history panel entries: Sketch, Extrusion, Fillet, Chamfer, Movement/Rotation, Pattern Circular, Mirror, Project).
- Autodesk Fusion 360 (desktop, timeline/browser visible): tongue & slot, flexible T-slot, eye slot with grip fins, "Snap In v1" locking tab, "Glue Pad v1/v2".
- A slicer layer-preview (orange/yellow/purple/red, grey bed, white grid; looks PrusaSlicer/OrcaSlicer-style but never named) shown at 2:50ish (glue-pad/top-surface), 12:xx-13:xx style, 28:15 (pin layer ends), 29:xx-30:xx (cross pin infill). A laptop stock clip at ~25:xx shows a vase in a slicer (generic b-roll).
- Links in description (not specified in video): print-on-demand page https://tinyurl.com/mycxwxs4 , filament https://tinyurl.com/bdcjjc9m , "Partner Designer" https://tinyurl.com/4aaz74pu , Shapr3D promo (code Slant3d, 10% off) https://tinyurl.com/pc2r8wcv. Sister channels: Slant POD, Tangled (materials testing). No CAD/STL files are linked anywhere.

Chapter list (from description): 0:00 Improving Pegs & Holes; 1:27 Low Profile Slab & Slot; 2:03 Snap Fits with S-Brackets & C-Clamps; 4:24 Basic Tongue & Slot; 5:29 "T" Tongue & Slot; 8:00 "I" Tongue & Slot with Grip Fins; 10:38 Bi-directional Locking Tabs; 13:26 Surface Features for Gluing; 15:53 Internal Glue Slots; 17:11 Simple Horizontal Pins & Holes; 19:27 Reduce Overhangs with Fins & Slots; 22:20 Flexible Fins for Better Tolerance; 24:59 Simple Vertical Pins & Holes; 27:40 Stronger Cruciform Pin & Slot; 30:01 Micro-features for Indestructible Vertical Pins.

Number-tagging convention: STATED = said aloud or legible on screen. ESTIMATED = my read from frames. NOT GIVEN = needed but absent.

---

## Global numbers that appear on screen

| Value | Where | Tag |
|---|---|---|
| 25.00 mm x 25.00 mm square block (Fusion, "Eye Slot and Tongue v1" sketch) | ~7:19 CAD cutaway | STATED (dimension callout) |
| Ø20.00 mm circle (eye slot / eye tongue) in the same sketch | ~7:19 | STATED (callout) |
| 10 mm x 10 mm square, copied/moved 15 mm (Shapr3D, "Normal to Sketch" on cube face) | ~1:40 | STATED (callouts "10 mm", "10 mm", "15 mm") |
| 8 mm wide rectangle (Shapr3D "Rectangle", Top view, 0.5 mm grid) | ~2:37 | STATED (callout "8 mm", lock icon); height not legible |
| Fusion extrude profile "Area: 6.00 mm^2" for the snap-tab slab | ~11:39-11:42 | STATED (status bar) |
| Fusion "Taper Angle 0.0 deg" field open in extrude dialog (value left at 0 in shown frames) | ~11:39 and glue pad ~13:31 | STATED but trivial |
| Glue pad cut distance "-0.5 mm" with Taper Angle field being edited (Fusion "Edit Feature", cutting small square holes) | ~13:26-13:31 | STATED (-0.5 mm); taper value not shown |
| Shapr3D "Extrusion 04": Distance 10 mm, Draft Angle 1.5 deg, Start From Profile, Result Union, Sides One-Sided, "9 faces" profile (the cross pin) | ~29:12 | STATED (panel legible in native frame) |
| Hole clearance vs pin: "about a quarter of a millimeter... sometimes up to half a millimeter" | 26:00 | STATED |
| Micro-feature slot width 0.2 mm | 30:37-30:48 | STATED |
| Chamfer on pin tip = consistent 45 deg overhang | 18:28 | STATED |
| Pin draft "slight draft angle", base wider than hole, top narrower | 29:02 | STATED qualitatively; 1.5 deg is only the Shapr3D panel value on the cross pin (ESTIMATED to be the same feature) |

Cube size of demo parts: ESTIMATED ~25 mm cubes (matches the 25.00 mm Fusion sketch and the 10 mm pin/tab sketches).

---

## Part A (0:00-4:24) Pegs and slots between parts (Shapr3D)

### A1. Diamond peg + diamond hole  (0:42-1:27)
- Purpose: simplest friction-fit locator between two printed parts, when glue may be added ("If you're going to use some glue, just go ahead and use a peg", 3:58).
- Geometry: a SQUARE peg rotated 45 deg ("turn it sideways") so it is a diamond; matching diamond hole. Rationale stated: round hole sags and ends up dimensionally off; diamond hole has "no overhang area so it's very dimensionally precise"; peg is printed horizontally so its layer lines run along the peg (strong). No dimensions stated. On screen (0:07-0:08) the two cubes joined by a small peg; ESTIMATED peg ~6-8 mm across, ~6 mm long.
- Print: peg part lies on its side (peg parallel to bed, "print the square peg horizontally on the print bed"); hole is in a vertical face. Held "only by the actual friction of the parts themselves". No settings.
- Failure modes: round peg printed horizontally is in-plane with layers and snaps off (1:00); round hole sags/oblong.
- CAD procedure: not demonstrated step by step; b-roll at 0:55 shows three printed rods (round, round-with-domed-end, hex/octagon-ish chamfered) for comparison.

### A2. Slab and slot ("low profile")  (1:27-2:03)
- Purpose: low-profile joint for thin parts or edge pegging, where small diamond holes are impractical.
- Geometry: a thin rectangular slab inserted into a matching rectangular slot. "Taper the ends... round it off so that it slides in and then gets tighter as it goes in cuz it can connect with the walls of the part even better." Dimensions not stated. On-screen Shapr3D sketches: 10 mm x 10 mm square on a cube face (1:40), later 8 mm wide rectangle (2:37). ESTIMATED slab thickness ~1.5-2 mm (6.00 mm^2 profile in the Fusion snap-in file suggests a slab cross-section of 6 mm^2 area, e.g. 3 mm x 2 mm, ESTIMATED).
- Print: thin gray test piece shown with a long narrow slot (0:29-0:33 b-roll). Orientation not stated.
- CAD procedure (Shapr3D, ~0:55-2:37): (1) sketch square/rectangle on a cube face ("Sketch plane 02", Normal to Sketch); (2) Move/Rotate with Copy to duplicate the sketch 15 mm along the axis (one copy for the male part, one for the female); (3) extrude one as slab/pin, cut the other as slot; (4) Chamfer/Fillet the slab tip ("Chamfer/Fillet Auto" tool visible at 3:31 on the S-bracket).

### A3. S-bracket (separate clip)  (2:03-3:09)
- Purpose: strongest and most precise of the Part A joints. A separate small S-shaped (zig-zag) printed piece; each part gets a slot; the S sits half in each and its hooked ends snap into small side pockets ("slide in the side bracket and then slide it into a slot to where it will snap into a small slot inside of the part").
- Symmetric, so same hole can be repeated everywhere. "You can change the size of the connector piece in order to increase the amount of compression." Round all corners; can be "as thick as you want to" for strength.
- Geometry: no numbers. Frames show S/Z zig-zag with two small end hooks (2:30 in b-roll at ~3:18 yellow zig-zag; native frame shows a single-bend Z with a hooked end). Shapr3D Line/Arc sketch, then Extrusion, then Chamfer/Fillet (3:31 frame shows an extruded Z with chamfer applied to an edge and a Move/Rotate gizmo reading 0.0 mm). ESTIMATED strip thickness ~1.5-2 mm, ~25 mm long.
- Print: lay the S flat (profile in XY) so layer lines run along the strip; he does not state it but the profile extrusion implies it (ESTIMATED).

### A4. Double-sided C-clamp snap fit  (3:09-3:58)
- Purpose: tool-free, intuitive snap; "pressing together", less robust than S because it is a mechanism (must flex and the latches must catch "just right").
- Geometry: C/U clip with two hooked tines that press into a slot and latch into holes inside the part (yellow part with a rectangular slot, clip with two hooks, frames 3:19-3:31).
- No numbers. Print flat; thickness tuned so tines flex.
- Comparison summary stated at 3:58: peg = easiest/glue; slab = thin profiles; S = strongest and tight; snap fit = fast and easy, no pressure needed, still tight.

Timestamps: A1 0:42; A2 1:27; A3 2:39 (spoken) / S b-roll 2:50-3:09; A4 3:19; summary 3:58.

---

## Part B (4:24-13:26) Tongue-and-slot family (Fusion 360)

### B1. Basic square tongue and slot  (4:24-5:28)
- Square tongue in square slot, slide or press. Verdict: "not very useful because they don't hold together very well" and "a lot of tolerance issues". Only advice: chamfer the insert slightly so it wedges in and the layer lines lock. No number.
- Fusion sketches: Tongue & Slot v1 file; sketch of a narrow rectangle plus a longer neck rectangle on a square face (frames 3:31-3:52 area / Fusion "Extrude" panel with New Body).

### B2. T-slot  (5:29-6:20)
- Tongue = T (neck + crossbar). Advantages: lateral support, cannot pull apart. Chamfer the top of the tongue so it angles up and locks. Problems: several tolerances (neck width, bar width, bar thickness), complex first layer that can warp/curl with high-warp materials, seam gap depends on shrinkage ("Based on material shrinkage... this won't always work").
- No dimensions.

### B3. Flexible (spring) T-slot  (6:20-8:00)  <- the one genuinely compliant joint
- Name in video: upgrade of the T-slot; file title in Fusion: "flexible t slot v1"; the video calls the curved wings "springs".
- Geometry: take the T and CURVE the two outer flanges so they act as leaf springs instead of rigid friction pads. Result: "no jiggle, no tolerance issues at all", tolerant to shrinkage.
- Print-orientation trick: "we went ahead and angled the slot" so the first layer is a simple filleted square (no thin T on the bed); "the rest of the complexity happens later in the print". "The two outer flanges are chamfered as well." Downside: a hole (open slot) in the bottom face of the part, acceptable for a non-customer-facing side.
- Numbers: none stated. Fusion frames: parts are ~25 mm cubes; the curved flange sketch is a circular arc (circle of diameter about 1.6-2x the neck, ESTIMATED from the 6:41 frame: an arc sketch centered on the neck axis, flanges tangent to it). Slot tilt angle ESTIMATED 20-30 deg off the bed normal; not stated.
- CAD procedure as shown (Fusion, 6:41-7:29): (1) Sketch1 on the part face for the slot; Sketch2 for the tongue neck+bar; extrude New Body; (2) new file "flexible t slot v1": draw a circle on the slot face and trim it to produce the curved flange profile (frame 6:41 shows circle with line through it and cut-off sides); (3) Sketch4 in Bottom view with a skewed/angled profile to angle the slot (7:06 bottom-view sketch showing a wedge at the left edge); (4) Fillet tool applied to 4 faces (Type Fillet, Radius Type Constant, Tangent chain on, Corner Type Rolling Ball, radius field being typed; value not captured); (5) Chamfer flanges.
- Material: not discussed beyond "high warp material". Flexure thickness/clearance: NOT GIVEN.

### B4. Eye ("I") slot with circular tongue  (8:00-9:33)
- Tongue = circle on a neck (keyhole). "Easier to design than the T slot because you're not doing all the XY tolerancing"; "one single circle that is dead center dimensionally to the other circle". Chamfer so they lock; layer lines bind. Also a simpler, curved first layer (low warp risk) if the tongue must be printed face-down.
- Weakness: short stumpy slots spread at the top (flex like a clamshell) - deepen slot, at the cost of insertion force.
- Numbers (STATED on screen, Fusion "Eye Slot and Tongue v1", ~7:19): block 25.00 x 25.00 mm, eye circle Ø20.00 mm. Neck width and depth not shown (ESTIMATED neck ~4-5 mm wide, ~8 mm long; ESTIMATED from the keyhole picture at 9:39 frame). Slot/bearing chamfer: "chamfer" only.

### B5. Eye slot with grip fins  (9:33-10:38)
- Name: "grip fins" ("small tabs all the way around the hole").
- Geometry: the circular eye pocket is lined with thin flexible fins that "cannot be connected to the roof of it" (they are detached from the top/bottom skin on one side, i.e. cantilevered springs). A larger-than-nominal eye tongue is pushed in and the fins grip and center it. Frames (8:23-9:39): about 14-16 fins, slanted tangentially like a camera iris or fan blades (ESTIMATED count 15, visible in the 8:23/8:38 Fusion frames), arranged around a ~20 mm circle, with a vertical slot opening on the right for the neck. Each fin chamfered on its leading edge (Fusion "Edit Feature: Two Distance chamfer" panel at 8:03, on a fin).
- Stiffness tuning: "making them thicker, making them longer" grips harder. Gives a semi-flexible joint (a little give/pivot) while still centering.
- Fin thickness/length/angle/count: NOT GIVEN (counts and angles above are ESTIMATED). He notes this geometry "is impossible" to machine/mold (10:50-11:09), so it is a printing-only feature.
- CAD procedure (Fusion): circle on face (Ø20.00), slot to the edge, then a single fin sketched (line pair), extruded as a thin body, chamfered, then circular-patterned around the circle (timeline in the 8:03-8:38 frames has many repeated features at the end = a pattern + per-fin chamfer). Exact pattern count: not stated.

### B6. Bi-directional locking tabs ("Snap In v1")  (10:38-13:26)  <- the creator's recommendation
- Rationale (11:09-12:03): combine eye-slot idea and grip fins into a joint that cannot be machined: the female hole has TWO internal recesses (undercut pockets) inside the cavity; the male part has two flexing flanges ("two little tongues") each with a locking bump. Push in, the flanges flex and the bumps snap into the recesses. "Bidirectional" = pull it back apart (building kit). Can instead be made permanent/non-releasing and tighter ("pull it in super tight so there is no flexure at all").
- Print specifics (12:13-12:44): the cube sits on the plate "like this" - the tab part is printed with tab/flanges projecting sideways, and "these flanges do not need any sort of support at all because we angled them on the bottom"; first layer is a simple square (no warping); parts "come off fully complete". Orientation: tab axis horizontal, flanges' lower surfaces angled (~45 deg ESTIMATED; "angled" only).
- Geometry from frames (11:39-12:56, Fusion "Snap In v1"): male tab = a rectangular stem with two thin flanges on opposite faces, each carrying a small triangular bump (chevron outward) - the 11:39 frame shows a "V" profile sketch (inverted-chevron) above/below a slab with 6.00 mm^2 profile; frame 12:17 shows the stem/flanges with 2 triangular bumps on each side as vertical ribs (2-3 grooves visible). Female part has matching rectangular cavity with two V recesses. Overall hole ~10 mm wide x ~10 mm tall (ESTIMATED from the 10 mm sketches); tab distance 19.00 mm in the extrude status bar at ~12:17 ("...in Distance: 19.00 mm" partly legible) - ESTIMATED reading.
- Four design variants shown side by side (10:50 and 11:07 frames): square tongue, eye (circle) tongue, T tongue, and the locking tab, all on 25 mm cubes.
- Material/tolerance: "You can change the tolerances so they pull tighter"; "fairly easy to tolerance". Not specified further. Uses "a smidgen less material", more reliable, easier to assemble.
- CAD procedure (Fusion timeline ~12 sketches): Sketch1-9 visible in the browser; extrude slab (New Body); sketch V profile on the slab edge; extrude as bump; mirror to the other side (frame at 12:56 shows the same V on top and bottom of the slab, Extrude dialog "New Body"); sketch the matching recess in the female cube (13:xx frame shows a rectangle with V reliefs), cut. Specific distances other than 19.00 mm and 6.00 mm^2 not captured.

---

## Part C (13:26-17:11) Glue-assist features (Fusion 360, "Glue Pad v1/v2")

### C1. Dovetail-style relief pockets on a glue surface  (13:34-15:15)
- Purpose: let adhesive mechanically key into a printed part. "Make a hole that gets wider as it goes in... hundreds of them and make them really small" - undercut pockets, so glue is "effectively able to grab onto the part mechanically rather than just through adhesion". They also give excess glue somewhere to go so the stated part tolerance is retained.
- Geometry: tiny square holes on a flat pad, pattern of about 15 x 15 grid (ESTIMATED count from the 14:30 frame: ~15-17 across, ~15 down); each cut -0.5 mm deep with a Taper Angle applied in the Extrude-cut dialog (so the hole widens as it goes deeper; angle value not shown). Cross-section view (14:38 frame) shows the pockets as shallow rectangular undercut slots just under the surface (a section of the pad with red hatch and rows of dark slots).
- Pad plate ESTIMATED ~60 x 60 x 5 mm; not stated.
- CAD procedure: sketch a square on the pad, extrude-cut -0.5 mm with taper angle, rectangular pattern across the pad ("Glue Pad v1"). v2 shows a different pad with a ring/circle feature (15:20 frame: circle sketch with centre point on the pad, ESTIMATED a circular glue-ring or gate) - not explained.

### C2. Directed glue patches  (15:15-15:50)
- Raised or recessed pattern marking where glue belongs "so fewer errors happen" in production; example is a pad with a circular groove plus a central dot (15:37-15:46 hand-held red part with ring/dot pattern). No numbers.

### C3. Internal glue channels  (15:53-17:11)
- Relief bead for hot glue (15:57-16:15), or an internal channel through an assembled part so glue can be injected after assembly ("shoot glue down from the top and it fills that entire channel"), including channels leading into a threaded-insert hole to deliver thread-lock (16:54-17:04). No dimensions. Not CAD-demonstrated.

---

## Part D (17:11-24:44) Horizontal pins and holes (Shapr3D b-roll, mostly spoken)

Stated rationale (17:23-18:09): printed horizontally, pin layer lines are in the plane of the layers => stronger than a vertical pin. Round pin straight out of a cube with a circular hole = holes sag oblong; unsupported circular pin needs support.

### D1. Basic good practice pin/hole  (18:09-19:27)
- Chamfer bottom of cube, round corners. Chamfer (not fillet) pin tip: "chamfer is a consistent overhang of 45 deg as opposed to a fillet which goes from infinite overhang to nothing". Fillet/lead-in on holes. Give the top of the hole "a small corner up on top... fairly shallow" (i.e. teardrop/peaked top so the hole keeps its shape, no sag): the Shapr3D b-roll at 18:14 and 18:30 shows a teardrop hole in the cube face. Support under the pin to keep it crisp. Verdict: still tolerance-sensitive across materials/settings/shrinkage (19:28-19:56).
- Numbers: none. 45 deg stated for the pin tip. Teardrop apex angle NOT GIVEN (ESTIMATED 90 deg i.e. 45 deg sides).

### D2. Keyhole pin with top+bottom chamfered flanges (fins)  (19:56-20:50)
- The sacrificial support under the pin is turned into part of the pin: pin gets chamfers on bottom AND top so it prints in any orientation without supports; mirrored on the other side so it is a "keyhole" (flat-sided ribbed pin). The flanges act as tension areas; the side walls (high-tolerance sliding surfaces) do the fit; top/bottom no longer interface with the hole. Frames 20:03-20:33 show the pin as an arrowhead/diamond profile: Shapr3D at 19:56-20:15 shows a cylinder with a triangular fin on top and bottom (arrow/pointed ends) fitting a vertical slot with a round middle.
- Printed demo (21:xx frames): red cubes joined with a pointed pin into a vertical slot.

### D3. Slot instead of circular pin  (20:50-21:26)
- "Why do you need a circular pin there at all?" Make it a slot/tab: only side compression of the hole interfaces with the tab. Rectangular extrusion, chamfered so no overhang in the rectangular hole. Printed demo: red cube with arrow-shaped tab into a rectangular slot (20:50-21:12 frames: orange tab into slot).
- Weakness: fit still depends on material.

### D4. Thicker, tapered, offset tab (self-centering wedge)  (21:26-22:08)
- Make the slot/tab thicker; chamfer the tab "slightly so that the top is narrower than the entryway to the hole and the bottom is wider than the entryway" so insertion gets progressively tighter; use "a couple of them slightly offset" so it self-centers. Not numerically specified. Purple demo cube (21:38-21:51).

### D5. Flexible fins / two-tab spring pin  (22:20-23:44)  <- compliant
- Replace the solid tab with TWO flexible tabs (forked, like a tuning-fork) that press against the slot's outer walls: "regardless of what machine you make it on, they will always work". Plain smooth tabs slide out, so add "a couple of small bumps and a couple of small holes inside of the slot" (detent bumps on the tab ends; matching dimples in the slot) so they "interlock and now you get a nice little popping". Demo: purple forked pin (22:29-22:53 frames: two prongs about 10 mm tall with small outward bumps at the tip).
- Numbers: NONE (tab thickness, gap between tines, bump height all NOT GIVEN). ESTIMATED from frames: prong width ~1.5-2 mm each, gap ~2 mm, overall pin ~6 mm wide, 10 mm tall, bump <0.5 mm.
- Print: horizontal, so tines flex across layers? Orientation not stated; the flexible fins' plane should contain the layers for strength (INFERENCE, not stated).

---

## Part E (24:59-32:29) Vertical pins and holes (Shapr3D)

### E1. Baseline "bad" pin (red cube)  (25:30-25:41)
- Plain cylinder, no fillet, hole same size as pin: "very poorly designed".

### E2. Corrected simple pin  (25:41-27:34)
Procedure/rules stated:
1. Fillet (funnel) at the top edge of the hole, "so it's possible for something to be pressed into it" (25:41).
2. Hole "a hair larger" than pin: "about a quarter of a millimeter. You can sometimes go up to a half a millimeter depending on shrinkage, but a quarter is generally fine" (26:00) - STATED. Interpretation: 0.25 mm (diametral vs radial not specified) default, 0.5 mm max.
3. Fatten the pin (bigger diameter) - diameter not given.
4. Fillet the base of the pin (matches the hole fillet), because the pin breaks at the base (26:28).
5. Round (fillet) the top of the pin so it locates in the hole (26:37).
6. Chamfer cube bottom edge, round outer corners (27:06).
7. Make the pin as short as possible (27:25-27:34) to cut the torsion lever arm.
Shapr3D demo (24:59-26:57, hand-held iPad frames): cube with pin extruded from the top face; Circle sketch with centre point; Extrude; Fillet; Chamfer; second cube with hole + chamfer; History list: Sketch 01, Extrusion 01, Fillet 01, Chamfer 01, Chamfer 02, Movement/Rotation 01, Sketch 02, Extrusion 02, Extrusion 03, Chamfer 03.
Numbers on screen: none legible for diameter/length (ESTIMATED pin Ø ~6-8 mm, ~8-10 mm tall).

Failure mode explained (27:43-28:04): force at the tip is a lever arm and the pin shears along layer lines at the base fillet corner.

### E3. Cruciform (plus-shaped) pin and slot  (27:40-29:33)
- Replace the round cross-section by a PLUS (cross) pattern: "same function, presses right into it... more strength because these individual sections give you more strength in the direction that the push is happening" - ribs run in-line with the load, vs only an outer skin on a cylinder where "as soon as a crack forms, it breaks on through".
- Draft/taper: "slight draft angle - make the base slightly wider than the hole, and the top narrower than the hole", so it starts easily and wedges. Cross also "wears in" so it conforms to the hole on repeated insertion and "there's not direct binding of the outer walls".
- Numbers (STATED on screen, Shapr3D Extrusion 04, native frame ~29:12): Sides One-Sided; Extent Distance 10 mm; Draft Angle 1.5 deg; Start From Profile; Result Union; Profile "9 faces" (the cross with fillet pockets). So cross height 10 mm, 1.5 deg draft - ESTIMATED to be the demo pin (it is the only pin extrusion with a visible number).
- Cross arm width/length: NOT GIVEN. ESTIMATED from the 29:24 frame: arms ~2-3 mm thick, overall span ~8-10 mm, base fillet visible (the pin tower also sits in a filleted counter-sink on the cube top).
- Hole: matching plus-shaped hole with chamfered/rounded lead-in; clearance as in E2 (0.25 mm). Printed grey and orange examples at 28:46-29:24; gray pin cube with plus-shaped pin and orange cube with plus slot (29:33 frame shows the gray plus pin and orange cube).
- Slicer view (29:52-30:08): layer preview of the cube top (red infill) with the cross rendered as purple inner perimeter loops (solid cross region surrounded by 2-3 perimeters) inside the cube's red infill; native frame 30:34 shows the plus having multiple concentric outlines with yellow+orange walls. This visualizes why a thin cross prints as nearly solid: it is only 2-3 perimeters wide.

### E4. Fluted / "wrinkled" circle pin with internal cross + micro-feature  (30:01-31:29)  <- final design
- "Maximum amount of material on the outer edge where the crack would want to form": circle whose perimeter is scalloped ("wrinkled outer edge") - Shapr3D shows a ~16-flute circular profile (ESTIMATED 16 half-circle notches, 30:34-30:56 frames, circular pattern; the frame at 30:56 shows ~16 orange fillet dots around the rim being selected for extrude) on top of a plain cylinder; plus an internal cross.
- Micro-feature: "you put a 0.2 mm slot into your model. And what will happen is that that effectively turns into walls inside of your model... apply solid areas to particular areas". Slots are driven "deep into this part a little ways" (below the pin base into the cube), so the pin becomes "effectively solid" while the cube remains regular infill. STATED slot width 0.2 mm. Depth/length of slots: NOT GIVEN.
- Details restated: chamfer + round top, base fillet, same hole rules as E2 (lead-in fillet, 0.25-0.5 mm clearance). Result "will press together and fit perfectly every single time, regardless of what color, what material".
- Shapr3D history list at 30:34 (right panel): Sketch 01, Extrusion 01, Fillet 01, Chamfer 01, Chamfer 02, Movement/Rotation 01, Sketch 03, Extrusion 03, Fillet 02, Sketch 03, Extrusion 04, Sketch 04, Extrusion 05, Sketch 05, Extrusion 06 - i.e. cube, pin base, scalloped pin extrusion, internal cross extrusions, micro slots (Sketch 05/Extrusion 06 probably the 0.2 mm cuts - ESTIMATED).
- Slicer screenshot at 30:56: a square cross-section showing a magenta/purple solid pattern (diagonal fill) = a 0.2 mm slot region turning into solid perimeters. A matching slicer view (31:07) of a solid-looking pin region.
- How the trick works in the slicer (reasoning, partially from video): a 0.2 mm gap is thinner than a 0.4 mm nozzle line, so the slicer treats the two sides as separate thin walls and does not infill between; he implies it converts to walls. Not shown with settings.
- Material: "regardless of what color, what material" - no specific polymer.

---

## Print-orientation, materials, slicer notes (everything the video states)

- Peg printed horizontally for strength (1:09, 17:33).
- Tongues printed so the first layer is a simple filleted square (6:57-7:19), done by angling the slot; for tongues that must be printed face-down use the eye/circular tongue (smooth curves, low warp) (9:10-9:22).
- Locking tab part sits on the bed, flanges angled on their underside so no supports (12:13-12:33).
- Chamfers (45 deg) beat fillets for any unsupported feature (18:28).
- Warping: high-warp materials curl on a complex first layer (5:49-6:11).
- Shrinkage and slicer/machine variation make fixed-clearance fits unreliable (6:11, 19:28-19:44, 28:35).
- No layer height, nozzle, wall count, infill %, material (PLA/PETG/TPU), temperatures, or support settings are stated. Demo parts appear to be PLA-like glossy/matte filaments in many colors (printed on the Slant farm), nothing else known.
- Failure modes mentioned: round hole sag/oblong; pin breaking at base along layer lines; first-layer warp on T tongue; spread/hinging of short tongues; plain flat tabs slide out; peg joints flex and leave a gap when pressed on broad faces (2:03-2:21), fixed by making stiffer (costly) or using S/C snap parts.

---

## GAPS (needed to reproduce, not given by the video)

General
- No layer height, nozzle diameter, extrusion width, perimeter count, infill, top/bottom layers, supports on/off (except "no support" claims), material, temperature, or printer/slicer for ANY part.
- No exported file or link to CAD/STL; "Partner Designer" link not described.
- Cube size never stated (25 mm is ESTIMATED from the 25.00 mm sketch).
- Clearance policy only given for the vertical pin hole (0.25-0.5 mm). Clearance for slab slot, tongues, T-slot, eye slot, locking tab, S-bracket, C-clamp: NOT GIVEN.

Per mechanism
- Diamond peg: peg size, depth, hole clearance, chamfer size.
- Slab and slot: slab thickness/width/length, taper angle, rounding radius, slot clearance (only 10 mm sketch squares and the 8 mm width shown).
- S-bracket: strip thickness, width, bend angles, hook depth, pocket size, interference ("compression") amount.
- C-clamp: tine thickness, hook geometry, hole spacing, flex travel.
- Basic tongue/slot and T-slot: neck width, bar width/thickness, chamfer size/angle, clearance.
- Flexible T-slot: flange thickness, flange arc radius, slot tilt angle, chamfer sizes, fillet radius (fillet panel visible but value not captured), interference.
- Eye slot: neck width, neck length, chamfer size, clearance (only 25.00 block and Ø20.00 circle).
- Grip fins: fin count (about 15 ESTIMATED), thickness, length, tilt angle, root attachment, gap to the roof, chamfer values, interference with the eye tongue, circular pattern count.
- Locking tab: tab width/height, flange thickness, bump height/angle, recess depth, lead-in angle, underside angle for no-support (stated only "angled"), interference, release force; only 6.00 mm^2 profile and a 19 mm distance (ESTIMATED) available.
- Glue pad: pocket size, pitch, count (~15 x 15 ESTIMATED), depth (-0.5 mm STATED), taper angle value, pad size, glue-ring dimensions; internal channel dimensions.
- Horizontal pin: pin diameter/length, chamfer size, teardrop apex angle, hole clearance, keyhole flange thickness/angle, slot dimensions, tab offset and taper values, flexible tab thickness/gap/bump size, detent pocket depth.
- Vertical pin: diameter, height, fillet/chamfer radii, base fillet radius, hole lead-in fillet radius, hole depth.
- Cross pin: arm width/length (1.5 deg draft and 10 mm height are from one Shapr3D panel, ESTIMATED to correspond), hole clearance for the cross, fillet radii.
- Fluted pin: flute count (16 ESTIMATED), flute radius, internal cross size, micro-slot depth/length/count, how deep below the pin base they go, and the slicer behaviour/settings (e.g. whether gap-fill or thin-wall detection is on).
- No force/retention measurements, no cycle-life data, no material comparison.
