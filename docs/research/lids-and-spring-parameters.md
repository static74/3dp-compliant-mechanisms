# Research: compliant lids, printed springs, metal springs, barbed plungers, and pause-to-capture

Scope: this file fills the GAPS listed in `video1-report.md`, which summarizes Slant 3D's "Design Compliant Lids for Perfect Tolerance Every Time" (https://www.youtube.com/watch?v=IZKh6lo9SP4). It also covers printed springs, small metal compression springs, one-way barbed plungers, and pausing a print to capture a spring. Research date: 2026-10-26.

## Evidence labels

Every number below carries one of four labels.

- **SOURCED**: the number appears in the cited source.
- **DERIVED**: the number comes from arithmetic on sourced inputs. The row names both the formula source and the data source.
- **SECONDARY**: the number came only from a search-engine summary or a non-primary blog. I did not read the original document. Treat these values as leads, not facts.
- **UNSOURCED — engineering judgment**: no source gave the number. I chose it.

Two conventions need stating up front, because the sources mix them.

- **Clearance convention.** Fictiv, Hubs and the print-in-place test reports do not say whether their gap is per side or diametral. This research file marks each such value "side convention not stated". The skill should declare one convention and use it everywhere. I recommend **per side** for flat faces and **diametral** for bores, stated explicitly each time.
- **Orientation convention.** Words like "vertical" and "horizontal" mislead, because sources use them for opposite things. Akaki Kuumeri's flexure is "always printed vertically", which means a standing wall that bends in the XY plane. Slant 3D calls the same thing "in plane". This research file states orientation only by the **bending plane**: a member must bend in the XY (layer) plane, so that each layer is a complete copy of the beam. A member must never bend so that its tension face pulls layers apart in Z.

## Key primary sources used

| Short name | What it is | URL |
|---|---|---|
| Slant V1 | Lids Vol. 2 video (the summarized video) | https://www.youtube.com/watch?v=IZKh6lo9SP4 |
| Slant Tol | "How to Design a Print with Perfect Tolerance EVERY Time" (12:35), auto-captions read in full | https://www.youtube.com/watch?v=XKrDUnZCmQQ |
| Slant Springs | "Top 4 Springs You Can Design with 3D Printing", captions read in full | https://www.youtube.com/watch?v=wpriGP45Unw |
| Slant Snap6 | "6 Ways To Make Snap Fits for 3D Printing", captions read in full | https://www.youtube.com/watch?v=rsfZgT3ZEI8 |
| Slant SnapMP | "Design Snap Fits for Mass Production 3D Printing", captions read in full | https://www.youtube.com/watch?v=6DkCCOc5O1Y |
| Slant LidTypes | "Types of Lids", captions scanned for numbers | https://www.youtube.com/watch?v=7YAylxQFe3k |
| Bayer | Bayer MaterialScience (now Covestro), "Snap-Fit Joints for Plastics – A Design Guide" (PDF, 26 pp.) | https://fab.cba.mit.edu/classes/S62.12/people/vernelle.noel/Plastic_Snap_fit_design.pdf |
| Akaki | Akaki Kuumeri, "3D Printed Flexures" (Core77 webinar slides) | https://s3files.core77.com/images/c77_webinar_series/Akaki-Kuumeri-3D-printed-flexures.pdf |
| He 2022 | Liang He, UW PhD dissertation on 3D-printable spring mechanisms (includes Ondulé) | https://makeabilitylab.cs.washington.edu/media/publications/He_FabricatingKineticObjectsWith3DPrintableSpringBasedMechanismsForInteractivity_UWCSPHDDISSERTATION2022.pdf |
| PLA TDS | Prusament PLA technical data sheet v1.1 (copy hosted by MatterHackers) | https://www.matterhackers.com/r/xFvGl8 |
| PETG TDS | Prusament PETG technical data sheet (copy hosted by a reseller) | https://www.3dprintergear.com.au/assets/files/technical-data-sheet%20(1).pdf |
| PS slice_z | PrusaSlicer source: layer slice plane = middle of layer | https://github.com/prusa3d/PrusaSlicer/blob/30ef59195e0f3ee6f270b185bb5f9fb5f349f81f/src/libslic3r/src/libslic3r/PrintObjectSlice.cpp#L62 |
| Cura PAH | Cura PauseAtHeight post-processing script source | https://github.com/Ultimaker/Cura/blob/5bea2f86153faed3a1c2d9081b8d6b753684678a/plugins/PostProcessingPlugin/scripts/PauseAtHeight.py |
| Lee WP | Lee Spring white paper, "Spring Design General Considerations" | https://www.leespring.com/sites/default/files/pdf/Lee%20Spring%20-%20WhitePaper%20-%20Spring%20Design%20General%20Consideration_US.pdf |
| Norton | R. L. Norton, Design of Machinery/Machine Design excerpt, "Buckling of Compression Springs" | https://designofmachinery.com/wp-content/uploads/2018/11/Ch144edp802.pdf |

## Derived material strain limits (used by Topics A, B and D)

The question these numbers answer is "how far can a printed beam bend before it yields or creeps out of shape?" The sources disagree, so the table shows each source and then the value I recommend.

| Parameter | Recommended value | Material / printer notes | Source URL |
|---|---|---|---|
| PLA elongation at yield, printed | 2.9 % (flat/horizontal specimens); 3.2 % (on-edge "vertical xz") | Prusament PLA, ISO 527-1. Modulus 2.3 GPa. HDT 55 °C. SOURCED | https://www.matterhackers.com/r/xFvGl8 |
| PETG elongation at yield, printed | 5.1 % (both orientations) | Prusament PETG, ISO 527-1. Modulus 1.5–1.6 GPa. HDT 68 °C. SOURCED | https://www.3dprintergear.com.au/assets/files/technical-data-sheet%20(1).pdf |
| Allowable strain rule, single snap | Amorphous plastics: up to ~70 % of yield strain. Semi-crystalline: almost to yield | Bayer guide, p. 11. SOURCED (rule) | https://fab.cba.mit.edu/classes/S62.12/people/vernelle.noel/Plastic_Snap_fit_design.pdf |
| Allowable strain rule, repeated use | ~60 % of the single-snap value | Bayer guide, Table 2 note, p. 12. SOURCED (rule) | same Bayer URL |
| Z-axis (across-layer) beam penalty | Halve the allowable strain; Z elongation at break drops ~50 % | Fictiv article. SOURCED | https://fictiv.com/?p=1238 |
| Fictiv "acceptable strain" table | PLA 4–8 %, ABS 7 %, Nylon 4–15 % | **Conflict:** Fictiv's PLA lower bound (4 %) exceeds the measured PLA yield strain (2.9 %). Do not use Fictiv's PLA number. SOURCED, but rejected | https://fictiv.com/?p=1238 |
| **PLA allowable strain, one-time snap** | **≈ 2.0 %** (XY-plane bending); ≈ 1.0 % if bending across layers | 2.9 % × 0.7. Treating printed PLA as amorphous is engineering judgment. DERIVED | Bayer URL + PLA TDS URL |
| **PLA allowable strain, repeated flexing** | **≈ 1.2 %** (XY); ≈ 0.6 % across layers | 2.0 % × 0.6. DERIVED | Bayer URL + PLA TDS URL |
| **PETG allowable strain, one-time snap** | **≈ 3.6 %** (XY); ≈ 1.8 % across layers | 5.1 % × 0.7. DERIVED | Bayer URL + PETG TDS URL |
| **PETG allowable strain, repeated flexing** | **≈ 2.1 %** (XY); ≈ 1.1 % across layers | 3.6 % × 0.6. DERIVED | Bayer URL + PETG TDS URL |
| Strain for a beam held deflected for days (creep) | ≤ 0.35–0.5 % | Akaki's flexure primitive (0.75 mm × 40 mm, 5 mm tip travel) works at 1.5·0.75·5/40² ≈ 0.35 %. Akaki: "Leave a flexure bent for a day, and it won't return to center"; "Never leave under tension." DERIVED from Akaki geometry; ceiling of 0.5 % is UNSOURCED — engineering judgment | https://s3files.core77.com/images/c77_webinar_series/Akaki-Kuumeri-3D-printed-flexures.pdf |
| Cantilever strain formula (constant section) | ε = 1.5·h·y / L², equivalently y = 0.67·ε·L² / h | h = thickness in the bending direction, y = tip deflection, L = length. Bayer Table 1, design 1. SOURCED | Bayer URL |
| Tapered beam bonus | Thickness tapering linearly to h/2 at the tip gives > 60 % more permissible deflection than a constant beam | Bayer p. 12. SOURCED | Bayer URL |

The derived rows are the numbers the skill should use. PLA allows roughly half the strain of PETG, and any beam that sits loaded for days should run at well under 1 % strain whatever the material.

---

## Topic A. Compliant lids (Slant 3D method)

### A.1 Resolving the 0.2 mm vs 0.3 mm relief gap

Video 1 showed 0.2 mm on screen and said ".3" aloud. Slant's longer tolerance video settles the question. At 5:27 Slant says to give "a gap underneath here of about .3", because a 0.3 mm gap survives "at any resolution". At 6:00–6:20 Slant adds that slicers and CAD exporters sometimes close a gap that small, that "you can go as large as .5, but at that point you can start to get deformation in your features", and that "3 is generally the best" (https://www.youtube.com/watch?v=XKrDUnZCmQQ&t=327).

PrusaSlicer's source code explains why 0.3 mm is the safe minimum. PrusaSlicer cuts each layer at the **middle** of that layer: `const double slice_z = layer_z_range.middle_z();` (https://github.com/prusa3d/PrusaSlicer/blob/30ef59195e0f3ee6f270b185bb5f9fb5f349f81f/src/libslic3r/src/libslic3r/PrintObjectSlice.cpp#L62). A horizontal gap therefore appears in the G-code only if at least one layer midpoint falls inside the gap.

- A gap at least one layer height tall always contains at least one midpoint, so it always survives.
- A gap shorter than one layer height may contain no midpoint, depending on where the layer boundaries fall. The slicer then fills the gap and fuses the fins to the flange.
- A 0.2 mm gap survives at 0.2 mm layers, but can vanish at 0.25–0.3 mm layers. A 0.3 mm gap survives at every common layer height up to 0.3 mm, which matches Slant's "any resolution" claim.

When the gap survives as exactly one empty layer, the first fin layer prints over air, one layer above the flange. The fin bottoms then behave like a support interface with a contact Z distance of one layer. Prusa says top contact distances of "50–75 % of the layer height seem to work well" for removable supports (https://help.prusa3d.com/article/support-material_1698). One full layer of gap is therefore enough for the fins to "break loose" (Slant V1, 3:39) with a light push. In short, design the gap as 0.3 mm, never less than one layer height, and never more than 0.5 mm.

A risk I did not verify: PrusaSlicer's "thick bridges" option prints the first layer over air with a round, nozzle-diameter-thick bead. The thick bead could sag into a one-layer gap and bond more strongly. The skill should tell the user to inspect the gap layer in the slicer preview.

### A.2 Table

| Parameter | Recommended value | Material / printer notes | Source URL |
|---|---|---|---|
| Bottom relief gap under fins, side springs and U-springs | **0.3 mm** (minimum 0.3, maximum 0.5); never less than one layer height | Slant says 0.3 mm survives any resolution; ≥ 0.5 mm lets features deform. SOURCED | https://www.youtube.com/watch?v=XKrDUnZCmQQ&t=327 |
| Why a sub-layer gap disappears | Slicer slices at layer mid-height, so a gap < 1 layer can contain no slice plane | PrusaSlicer `slice_z = middle_z()`. SOURCED (code); the gap rule is DERIVED | https://github.com/prusa3d/PrusaSlicer/blob/30ef59195e0f3ee6f270b185bb5f9fb5f349f81f/src/libslic3r/src/libslic3r/PrintObjectSlice.cpp#L62 |
| Gap at exactly one layer (0.2 mm at 0.2 mm layers) | Survives as one empty layer; fin bottoms print like a support interface and break free | Prusa: removable contact distance 50–75 % of layer height. DERIVED | https://help.prusa3d.com/article/support-material_1698 |
| STL export of the 0.3 mm gap | Export at fine tessellation and check the mesh; Slant saw an STL "modified … to create these artifacts that kind of close up those holes" | SOURCED (Slant Tol 5:43–6:00) | https://www.youtube.com/watch?v=XKrDUnZCmQQ&t=343 |
| Grip fin thickness | **Two perimeters at the slicer's thin-wall value: ≈ 0.86 mm for 2 perimeters with a 0.4 mm nozzle at 0.2 mm layers** (Akaki uses 0.75 mm for "exactly two lines") | Prusa: two 0.45 mm perimeters at 0.2 mm layers give a 0.86 mm wall, not 0.90. Match the slicer's own value so no gap fill prints in the fin. SOURCED (both numbers) | https://help.prusa3d.com/article/extrusion-width_1748 ; https://s3files.core77.com/images/c77_webinar_series/Akaki-Kuumeri-3D-printed-flexures.pdf |
| Minimum printable fin | A solid feature thinner than Arachne's "Minimum feature size" is dropped entirely; a fin just above it is widened to the "Minimum perimeter width" | Arachne: "Features thinner than this value will not be printed." The setting governs thin solids, not slots. SOURCED | https://help.prusa3d.com/article/arachne-perimeter-generator_352769 |
| Minimum slot between fins or behind an arm | ≥ one extrusion width (≈ 0.45 mm for a 0.4 mm nozzle); prefer ≥ 0.9 mm, as the pitch row gives | PrusaSlicer's "slice gap closing radius" (default reported as 0.049 mm, SECONDARY) merges gaps smaller than itself. Slot minimum UNSOURCED — engineering judgment | https://forum.prusa3d.com/forum/prusaslicer/vase-mode-bug/ |
| 0.6 mm nozzle adjustments | Beam thickness = two perimeters at the slicer's recommended thin-wall value for the active nozzle and layer height (≈ 1.2–1.3 mm for 0.6 mm). At constant strain and deflection, L scales with √t, so fins and arms grow about 20–25 %. The relief gap must still be ≥ one layer height: a 0.3 mm gap can vanish at the 0.32–0.4 mm layers common with a 0.6 mm nozzle, so use 0.4–0.5 mm (Slant's 0.5 mm maximum caps it) | DERIVED from the Prusa extrusion-width rule, the Bayer formula, PrusaSlicer `slice_z`, and Slant's 0.5 mm limit | https://help.prusa3d.com/article/extrusion-width_1748 ; https://www.youtube.com/watch?v=XKrDUnZCmQQ&t=360 |
| Grip fin length (root to tip, in XY) | **≥ 10.5 mm at 45°, ≥ 9.5 mm at 30°** (for 0.3 mm interference); ≥ 8.5 mm at 45° for 0.2 mm interference | A closed lid holds its fins deflected, so the held-deflection ceiling (≤ 0.5 % strain) applies. L = √(1.5·t·(δ/cos φ)/0.005) with t = 0.86 mm. Video 1 shows a 9.3973 mm length readout during the fin cut (ESTIMATED that it is the fin length); at 9.4 mm, 45° and 0.3 mm interference, strain ≈ 0.6 %, slightly above the ceiling, so Slant's design relies on its qualitative claim that the fins "lose almost none" of their pressure. The plug wall must be at least L·sin φ deep to house the fins (≈ 7.4 mm at 45°, ≈ 4.75 mm at 30° for L = 9.5). DERIVED | https://www.youtube.com/watch?v=IZKh6lo9SP4&t=212 + Bayer formula + Akaki URL |
| Grip fin slant angle | **30–45° from the wall surface** (not radial) | A radial fin (90°) cannot bend under radial interference; it can only buckle. A fin at angle φ needs bending deflection ≈ δ / cos φ to absorb radial interference δ. Video 1 estimate 45 ± 10°. Angle rule is DERIVED (geometry); the range is UNSOURCED — engineering judgment | https://www.youtube.com/watch?v=IZKh6lo9SP4&t=236 |
| Grip fin pitch | **2.5–3 mm** (0.4 mm nozzle) | At 45°, pitch 2.5 mm leaves a perpendicular slot of 2.5·sin45° − 0.86 ≈ 0.9 mm, wide enough not to fuse. Pitch 2.5 mm on a 75 mm plug side gives ~30 fins, which matches the 25–30 fins counted in video 1. DERIVED / UNSOURCED — engineering judgment | — |
| Fin-tip interference over the opening | **0.2–0.3 mm per side** (PLA and PETG) | Must exceed the worst expected undersize of the box opening plus a gripping preload, while keeping held strain ≤ 0.5 % (ε = 1.5·t·(δ/cos φ)/L²). Larger interference (0.5 mm per side) gives ≈ 1 % strain at L = 9.4 mm and 45°; accept it only for a lid that is opened often and never left closed for long, in PETG. UNSOURCED — engineering judgment; strain DERIVED | — |
| Fin creep | Slant: grip fins resist creep because "the pressures are distributed … against a lot of grip fins" and "they're deflecting so little" | SOURCED (qualitative) | https://www.youtube.com/watch?v=XKrDUnZCmQQ&t=646 |
| Fin corners | Leave the four plug corners solid (no fins) and rounded | Video 1 frame at 3:12. SOURCED (visual) | https://www.youtube.com/watch?v=IZKh6lo9SP4&t=192 |
| Side-spring arm length | **20–25 mm** (video 1 sketch reads 22.5 mm, ESTIMATED) | Constant strain means deflection scales with L²: Akaki's 5 mm at 40 mm becomes ~2 mm at 25 mm. DERIVED | https://www.youtube.com/watch?v=IZKh6lo9SP4&t=127 ; Akaki URL |
| Side-spring arm thickness | **1.2–1.6 mm** for a lid that holds; thinner for a loose fit | Slant: thicken for tighter, thin for looser (2:26–2:35). At 1.2 mm × 22.5 mm with 0.8 mm nub deflection, strain ≈ 0.28 %. Value UNSOURCED — engineering judgment; formula DERIVED | https://www.youtube.com/watch?v=IZKh6lo9SP4&t=146 |
| Side-spring slot width behind the arm | **≥ nub height + 0.5 mm, typically 1.5–2.5 mm** | The arm must reach full deflection before it bottoms out. Video 1 shows ~2.5 mm (ESTIMATED). UNSOURCED — engineering judgment | — |
| Side-spring tip and slot fillet | R1 mm | On screen in video 1 at 2:27. SOURCED | https://www.youtube.com/watch?v=IZKh6lo9SP4&t=147 |
| Side-spring nub | **Ø2 mm, 0.5–0.8 mm proud**, rounded, seating in a dimple 0.2 mm shallower than the nub height | Video 1 shows ~2 mm nubs (ESTIMATED). Dimple depth UNSOURCED — engineering judgment | https://www.youtube.com/watch?v=IZKh6lo9SP4&t=156 |
| Arm and fin root fillet | ≥ 0.5 × beam thickness (Hubs); never below 0.38 mm (0.015 in, Bayer) | SOURCED | https://www.hubs.com/knowledge-base/how-design-snap-fit-joints-3d-printing ; Bayer p. 8 |
| U-shaped / split "thumb" springs | Same 0.3 mm gap under the spring; soften by splitting, stiffen by thickening or pushing the shoe outward | SOURCED (qualitative) | https://www.youtube.com/watch?v=XKrDUnZCmQQ&t=391 |
| Perforated / scalloped plug | Scallop Ø 8–10 mm at ~15 mm pitch on a 75 mm plug (video 1 estimate), depth 1–2 mm into the wall, leaving 3–5 mm flat contact lands | Slant gives no numbers. Alternative from Slant Tol: hollow the plug to thin walls and touch only at the four corners (4:40). Values UNSOURCED — engineering judgment | https://www.youtube.com/watch?v=XKrDUnZCmQQ&t=280 |
| Thin-wall plug instead of solid | Cut out the plug interior so infill cannot change the wall's shrinkage | Slant Tol 3:36–4:08. SOURCED (qualitative) | https://www.youtube.com/watch?v=XKrDUnZCmQQ&t=216 |
| Lead-in on the plug top | Small chamfer or fillet on the plug's top outer edge so the lid "will at least start and then it can be pressed in the rest of the way" | Slant Tol 2:06–3:22 and Slant LidTypes 1:00. Size not given; use 0.5–1.0 mm × 45° (UNSOURCED — engineering judgment) | https://www.youtube.com/watch?v=XKrDUnZCmQQ&t=126 |
| First-layer chamfer (elephant-foot relief) | **0.4–0.6 mm × 45°** on every bed-touching edge | Slant: "always add a chamfer to the bottom of any given part" (Slant Tol 1:51). Prusa elephant-foot compensation starts at ~0.2 mm for a 0.4 mm nozzle, so the chamfer should be at least that. 0.5 mm × 45° is SECONDARY | https://www.youtube.com/watch?v=XKrDUnZCmQQ&t=111 ; https://help.prusa3d.com/article/elephant-foot-compensation_114487 ; https://siddament.com.au/blogs/filament-guide-au/fix-elephants-foot |
| Vertical corner radius | Round all vertical edges (video 1 derives R5 mm on an 85 mm lid) to avoid the "bang bang" direction change at sharp corners | SOURCED (Slant Tol 1:18–1:51); R5 DERIVED in video 1 report | https://www.youtube.com/watch?v=XKrDUnZCmQQ&t=78 |
| Rigid plug-to-opening clearance, box printed separately | **0.3–0.4 mm per side** for the plug body; let fins or springs supply the grip | Fictiv: 0.2 mm tight, 0.3 mm close snap, 0.4 mm slide (side convention not stated). Hubs: 0.5 mm nominal for FDM snap fits (side convention not stated). Print-in-place tests on Prusa MK3S+ and Bambu A1 in PLA: 0.2 mm moves freely (SECONDARY). Chosen range UNSOURCED — engineering judgment | https://fictiv.com/?p=1238 ; https://www.hubs.com/knowledge-base/how-design-snap-fit-joints-3d-printing |
| Corner relief splits in the box | Small slits at box corners let walls splay; keep them at 90° to each other and never design for ~0.5 mm splay, which splits layers | SOURCED (Slant Tol 9:08–9:39) | https://www.youtube.com/watch?v=XKrDUnZCmQQ&t=548 |
| Latch travel class | "almost 2 mm" for internal spring latches | SOURCED (video 1, 4:54). Confirmed by arithmetic in Topic B | https://www.youtube.com/watch?v=IZKh6lo9SP4&t=294 |
| Roof over a latch cavity | Design the roof so it cannot droop onto the latch; a sagging bridge "can make the latch jam" | SOURCED (video 1, 4:45) | https://www.youtube.com/watch?v=IZKh6lo9SP4&t=285 |

### A.3 Geometry that matters more than any number

- **Fin direction.** The fins must stand as vertical blades whose whole outline lies in each layer. Each fin then bends in XY, and layers run along the fin. A fin that bends in Z peels layers apart.
- **Fin slant.** The slant turns radial interference into bending. Without slant, the box wall loads the fin along its axis, and the fin either buckles or does not yield at all.
- **One gap, two jobs.** The 0.3 mm bottom gap frees the fins from the flange, and it also controls how much the fin bottoms droop. Do not enlarge the gap to make fins "freer"; enlarge the fin length instead.
- **Rigid locator plus compliant grip.** Slant's preferred pattern keeps a square, rigid base to locate the lid and puts compliance above it (Slant Tol 7:15). The rigid part takes alignment, and the compliant part takes tolerance.

The point of Topic A is that the gap size comes from slicer mechanics, while every other fin and spring dimension comes from keeping strain low.

---

## Topic B. Printed springs for FDM

| Parameter | Recommended value | Material / printer notes | Source URL |
|---|---|---|---|
| Master orientation rule | All spring force must lie in the layer plane; "if you try to print this spring at an angle you just ruined the spring" | Slant Springs 4:23–4:56. SOURCED | https://www.youtube.com/watch?v=wpriGP45Unw&t=263 |
| Cantilever / snap arm orientation | Turn the arm on its side so it flexes along the layer lines | Slant Snap6 1:17–1:37; Slant SnapMP 0:55–1:35. Hubs: avoid cantilevers built in Z. SOURCED | https://www.youtube.com/watch?v=rsfZgT3ZEI8&t=77 ; https://www.hubs.com/knowledge-base/how-design-snap-fit-joints-3d-printing |
| Geometries that work | Serpentine/zigzag flat-pack extension spring; planar leaf spring; ring/"trampoline" leaf spring; spiral (clock) spring; side-turned cantilever snaps | All printed flat, flexing in XY. SOURCED (Slant Springs) | https://www.youtube.com/watch?v=wpriGP45Unw |
| Printed helical coil spring | **Two views.** Slant: "the one spring that we will never make is a coil spring"; printed vertically its layers split. He 2022 (Ondulé): helical springs work if printed with the spring axis perpendicular to Z (lying on its side); "90° yields the highest" modulus | Use metal for helical compression springs (Topic C). Printed helical springs are a fallback, lying on their side. SOURCED (both) | https://www.youtube.com/watch?v=wpriGP45Unw&t=14 ; He 2022 URL, p. 69 and p. 124 |
| Minimum printed helical spring | Wire 1.6 mm, overall Ø ≥ 4.0 mm (Ondulé, 0.4 mm tolerance) | SOURCED | He 2022 URL, p. 124 |
| Wave spring | No FDM source found. Avoid; its crests load across layers in any orientation | UNSOURCED — engineering judgment | — |
| Torsion / spiral spring | Works when printed flat (spiral in XY). Thicken the strip in Z for more stiffness without raising strain | SOURCED (Slant Springs 5:05–6:02) | https://www.youtube.com/watch?v=wpriGP45Unw&t=305 |
| Serpentine beam thickness | Down to 1 mm for soft springs; thicker for stiff ones | Slant Springs 2:20. SOURCED | https://www.youtube.com/watch?v=wpriGP45Unw&t=140 |
| Serpentine corners | Round every bend; square bends concentrate stress and break "just below the curve" | SOURCED | https://www.youtube.com/watch?v=wpriGP45Unw&t=62 |
| Minimum flexure thickness vs nozzle | **Two perimeters at the slicer's recommended thin-wall value for the active nozzle and layer height: 0.75 mm (Akaki) to 0.86 mm (Prusa) for a 0.4 mm nozzle; ≈ 1.2–1.3 mm for a 0.6 mm nozzle (DERIVED).** At constant strain and deflection, beam length scales with √t, so 0.6 mm-nozzle springs need ~20–25 % more length. Akaki: single lines are hard to slice; "thicker than three lines suffers from non-isomorphism" | SOURCED | Akaki URL ; https://help.prusa3d.com/article/extrusion-width_1748 |
| Flexure width (in Z, i.e., the beam's depth) | ≥ 10 mm; narrower twists too easily | Akaki. SOURCED | Akaki URL |
| Flexure length | ≥ 40 mm for Akaki's 5 mm-travel primitive; shorter "doesn't bend well", much longer may bend in several places | Akaki. SOURCED | Akaki URL |
| L/t ratio | Akaki primitive: 40/0.75 ≈ **53**. Classical beam formulas are accurate above L/t ≈ 10 (BASF). Sovol suggests 8–10:1 for PLA and 5–8:1 for PETG snaps (SECONDARY) | Use L/t ≥ 10 so the formulas hold, and ≥ 25 for long-term springs. DERIVED / SOURCED | Akaki URL ; https://ulprospector.ul.com/1248/snapfit-3/ ; https://www.sovol3d.com/blogs/news/3d-printed-snap-fit-joints-how-to-design-clips-that-work |
| Allowable strain by material | PLA 2.0 % one-time / 1.2 % repeated; PETG 3.6 % / 2.1 %; held deflection ≤ 0.35–0.5 % | See the derived table above. Nylon, PP and TPU: no printed-specimen yield data found; Hubs names ABS, nylon and TPU as the strain-resistant FDM choices. DERIVED / SOURCED (qualitative) | Bayer + TDS URLs ; https://www.hubs.com/knowledge-base/how-design-snap-fit-joints-3d-printing |
| PLA creep | Akaki: PLA and common plastics "yield easily" and "creep easily". A PLA bag-clip spring plastically deformed after 20 days (SECONDARY, community report) | Keep PLA springs unloaded at rest. PLA HDT is 55 °C, so a warm car or sunny window accelerates creep. SOURCED (Akaki, TDS) | Akaki URL ; https://www.matterhackers.com/r/xFvGl8 |
| PETG vs PLA | PETG yields at 5.1 % vs 2.9 % and has HDT 68 °C vs 55 °C. Akaki: PETG "is said to be more flexible (yields later, creeps less) but in my experiments not a big difference" | PETG is the default spring material; PLA+ is acceptable for short-lived or rarely flexed parts. SOURCED | TDS URLs ; Akaki URL |
| Travel for a ~2 mm latch | At 0.86 mm thickness, 2 mm tip travel needs L ≈ **11.4 mm** (PLA one-time), **14.7 mm** (PLA repeated), **11.1 mm** (PETG repeated), **27 mm** (held for days at 0.35 %) | L = √(1.5·h·y/ε). Akaki scaling (5 mm at 40 mm, 0.75 mm thick) gives 2 mm at ~25 mm. Both confirm the ~2 mm latch class with a 15–25 mm arm. DERIVED | Bayer URL ; Akaki URL |
| Fatigue life | No FDM flexure S-N data found. Qualitative only: Slant says layer-aligned springs will not fatigue; one guide says PLA fatigues "after a few cycles"; BASF's fatigue cases speak of "hundreds or thousands of cycles" | Design for low strain (≤ 1 % PLA, ≤ 2 % PETG) and test. UNSOURCED for cycle counts | https://www.youtube.com/watch?v=6DkCCOc5O1Y&t=86 ; https://ulprospector.ul.com/1248/snapfit-3/ |
| End stops | Add hard stops so the user cannot overbend a flexure; printed plastic "yields early" | Akaki. SOURCED | Akaki URL |
| Seam placement | Keep the perimeter seam away from the flexure; use filleted corners as seam attractors | Akaki. SOURCED | Akaki URL |
| Flat-printed flexures | If a flexure must lie flat, make the print lines run lengthwise | Akaki. SOURCED | Akaki URL |
| First layer of flat springs | Tie thin spring tips to the body with a ~0.3 mm connector or mouse ears so the nozzle does not peel them | Slant Snap6 4:25–5:06. SOURCED | https://www.youtube.com/watch?v=rsfZgT3ZEI8&t=265 |
| Overhang above a spring | Replace a flat 90° overhang over a spring with a 45° chamfer so it does not sag onto the spring | Slant Snap6 5:02 and 11:34. SOURCED | https://www.youtube.com/watch?v=rsfZgT3ZEI8&t=302 |
| Breakaway support for side-turned snaps | Design your own ~1 mm diameter tie support under the snap nub instead of slicer supports | Slant SnapMP 2:19–2:29. SOURCED | https://www.youtube.com/watch?v=6DkCCOc5O1Y&t=139 |

### B.1 Method notes

- **Printed springs as embedded parts.** Slant points out that flat-printed springs can be printed inside the part, fully enclosed, which no other process can do (Slant Springs 6:18). Embedding works only when the spring's bending plane is the layer plane.
- **Choose metal when the spring holds load at rest.** A printed spring that stays compressed loses force through creep. A detent or plunger that rests preloaded should use a metal spring (Topic C) and keep the printed parts rigid.

Printed springs work when they bend in the layer plane at low strain; anything else, and any spring that stays loaded, belongs in metal.

---

## Topic C. Metal compression spring for a plunger, latch or detent

### C.1 Verified stock springs (Lee Spring LC series, stainless steel ASTM A313, squared and ground ends)

All values come from the Lee Spring product pages. "Hole" is Lee's catalog "Hole Diameter" field, which is the hole the spring is rated to work in. Lf/Dm is the buckling slenderness ratio, using mean coil diameter Dm = OD − d (Norton defines the ratio with mean diameter, not OD).

| Part no. | OD mm | Wire d mm | Free length mm | Rate N/mm | Solid height mm | Lee hole mm (hole − OD) | Lf/Dm | Source URL |
|---|---|---|---|---|---|---|---|---|
| LC 014A 05 S | 3.05 | 0.36 | 12.70 | 0.75 | 3.96 | 3.18 (+0.13) | 4.7 → guide | https://www.leespring.com/product/compression-spring-lc014a05s-stainless-steel |
| LC 016A 05 S | 3.05 | 0.41 | 12.70 | 1.24 | 5.21 | 3.18 (+0.13) | 4.8 → guide | https://www.leespring.com/product/compression-spring-lc016a05s-stainless-steel |
| LC 016A 09 S | 3.05 | 0.41 | 19.05 | 0.74 | 7.75 | 3.18 (+0.13) | 7.2 → guide | https://www.leespring.com/product/compression-spring-lc016a09s-stainless-steel |
| LC 018B 05 S | 4.57 | 0.46 | 12.70 | 1.02 | 3.35 | 4.78 (+0.21) | 3.1 | https://www.leespring.com/product/compression-spring-lc018b05s-stainless-steel |
| LC 022B 05 S | 4.57 | 0.56 | 12.70 | 2.05 | 4.78 | 4.78 (+0.21) | 3.2 | https://www.leespring.com/product/compression-spring-lc022b05s-stainless-steel |
| LC 018B 09 S | 4.57 | 0.46 | 19.05 | 0.58 | 5.05 | 4.78 (+0.21) | 4.6 → guide | https://www.leespring.com/product/compression-spring-lc018b09s-stainless-steel |
| LC 026BC 08 S | 5.33 | 0.66 | 20.65 | 1.45 | 8.74 | 5.56 (+0.23) | 4.4 → guide | https://www.leespring.com/product/compression-spring-lc026bc08s-stainless-steel |
| LC 020C 05 S | 6.10 | 0.51 | 12.70 | 0.72 | 3.35 | 6.35 (+0.25) | 2.3 | https://www.leespring.com/product/compression-spring-lc020c05s-stainless-steel |
| LC 022C 05 S | 6.10 | 0.56 | 15.88 | 1.02 | 3.94 | 6.35 (+0.25) | 2.9 | https://www.leespring.com/product/compression-spring-lc022c05s-stainless-steel |
| LC 026C 05 S | 6.10 | 0.66 | 15.88 | 1.82 | 5.16 | 6.35 (+0.25) | 2.9 | https://www.leespring.com/product/compression-spring-lc026c05s-stainless-steel |
| LC 020C 09 S | 6.10 | 0.51 | 19.05 | 0.47 | 4.62 | 6.35 (+0.25) | 3.4 | https://www.leespring.com/product/compression-spring-lc020c09s-stainless-steel |
| LC 022D 03 S | 7.62 | 0.56 | 15.88 | 0.74 | 3.10 | 7.95 (+0.33) | 2.2 | https://www.leespring.com/product/compression-spring-lc022d03s-stainless-steel |

LC 022B 05 S lists a maximum load of 14.82 N at solid height, so Lee rates these parts to solid (SOURCED, same URL).

Not verified, page not fetched: McMaster-Carr 9657K-series, McMaster 52022N128, Century Spring B18-190CS and 70785S, and Amazon assortment kits. Search summaries mentioned them, but I could not load the catalog pages. Do not publish those part numbers without checking them.

### C.2 Design rules

| Parameter | Recommended value | Material / printer notes | Source URL |
|---|---|---|---|
| Spring OD grows under compression | Calculate OD at the compressed length and check it against the hole, using the high side of the OD tolerance | Lee WP step 3. SOURCED | Lee WP URL |
| Commercial OD tolerance | 0.119–0.250 in OD: +0.003 / −0.005 in (+0.08 / −0.13 mm); 0.251–0.299 in: ±0.005 in; 0.300–0.500 in: ±0.008 in (±0.20 mm) | Lee WP step 9. SOURCED | Lee WP URL |
| Metal-hole clearance (catalog) | +0.13 mm at 3 mm OD, +0.21 mm at 4.6 mm, +0.25 mm at 6.1 mm, +0.33 mm at 7.6 mm, +0.39 mm at 9.1 mm (diametral) | Lee "Hole Diameter" minus OD, from the table above. DERIVED | Lee product URLs |
| Printed bore diameter over spring OD | **Lee hole + 0.2–0.3 mm, i.e., OD + 0.35–0.6 mm diametral** | Hubs: "FDM often prints undersized vertical-axis holes." The added 0.2–0.3 mm is UNSOURCED — engineering judgment; print a test bore | https://www.hubs.com/knowledge-base/how-design-parts-fdm-3d-printing/ |
| Guide-rod (pin inside spring) diameter | ≤ Lee "Rod Diameter" (e.g., 2.06 mm for LC 016A; 3.45 mm for LC 018B; 4.75 mm for LC 022C) minus 0.2 mm for a printed pin | Lee pages list rod diameter. Printed-pin allowance UNSOURCED — engineering judgment | Lee product URLs |
| Buckling threshold | Lf/Dm > 4 may buckle; a hole or rod prevents gross buckling, but coil rubbing costs force. A spring with one end free to tip buckles at a lower ratio | Norton. SOURCED | Norton URL |
| Buckling rule for the skill | Lf/Dm ≤ 4 with both ends seated flat: no guide needed. Lf/Dm > 4, or a tipping end: run the spring in a bore or over a pin | DERIVED from Norton | Norton URL |
| Usable deflection band | Load the spring between ~15 % and 85 % of its full deflection (free length minus solid height); both ends of the range are non-linear | SECONDARY (Scribd copy citing Shigley) | https://www.scribd.com/document/413988168/Spring-Design |
| Preload at installed length | **15–25 % of full deflection** so the plunger never rattles; never compress past 85 % in service | Example: LC 018B 05 S has 9.35 mm of full deflection, so install at ~11.0 mm (1.7 mm, ~1.7 N preload) and keep at least 1.4 mm from solid. UNSOURCED — engineering judgment, consistent with the 15–85 % band | — |
| Stress check | If stress at the working or solid height exceeds 40 % of tensile strength, expect set; above 60 %, redesign | Lee WP steps 7–8. Catalog parts rated to solid already pass. SOURCED | Lee WP URL |
| Solid height with tolerance | Allow +5 % on nominal solid height | Lee WP step 6. SOURCED | Lee WP URL |

Size the printed bore from Lee's hole value plus a printing allowance, guide any spring longer than four mean diameters, and preload it a little without ever running it to solid.

---

## Topic D. Plunger retention with one-way barbs (snap-in, cannot back out)

| Parameter | Recommended value | Material / printer notes | Source URL |
|---|---|---|---|
| Insertion (lead-in) face angle | **30°** from the insertion axis (range 20–45°) | Bayer's worked cantilever example uses α = 30° (p. 15); Bayer's annular example rounds a 45° edge and treats it as effectively 30°. firstmold gives 20–30° typical, 30–45° allowed with more force (SECONDARY) | Bayer URL ; https://firstmold.com/tips/snap-fits/ |
| Retention (return) face angle | **90°** for a plunger that must never back out | A 90° return angle "cannot be disassembled except through an external window" (Fictiv). Return faces of 60–90° are effectively inseparable; ≤ 45° are separable (Bayer-citing patent, SECONDARY). BASF uses a 90° return angle "to avoid bending" in its example | https://fictiv.com/?p=1238 ; https://patents.justia.com/patent/9049905 ; https://ulprospector.ul.com/1248/snapfit-3/ |
| Barb height (undercut) | y ≤ 0.67·ε·L²/h for a constant prong, about 1.6× that for a prong tapering to h/2. Example: L = 8 mm, h = 1.2 mm gives **0.7 mm (PLA, ε = 2 %)** or **1.3 mm (PETG, ε = 3.6 %)** | Bayer Table 1 with the derived one-time strains. DERIVED | Bayer URL + TDS URLs |
| Counterbore size behind the neck | Counterbore radius ≥ neck radius + barb height + 0.2–0.3 mm, so the prongs spring fully open and the barbs slide freely through the whole stroke | Bayer: after joining, snap features "should return to a stress-free condition" (p. 3). A barb that rubs the counterbore wall stays deflected, drags, and creeps. Margin UNSOURCED — engineering judgment | Bayer URL |
| Bearing overlap on the 90° face | Overlap = barb height − (body-to-neck radial clearance); keep **≥ 0.5 mm** | Rounded FDM edges eat into a small overlap. UNSOURCED — engineering judgment | — |
| Catch face as printed | Never chamfer the 90° catch face. If the housing prints bore-up, the step under the neck is a downward annular overhang: keep the annulus small (≤ 1 mm radial) and check it for droop, or print the bore horizontal or opening-down | Slant's usual fix (45° chamfer on overhangs) would turn the retention face into a release ramp. UNSOURCED — engineering judgment | https://www.youtube.com/watch?v=rsfZgT3ZEI8&t=302 |
| Prong (barb beam) thickness and length | h = 1.0–1.5 mm (2–3 perimeters), L = 8–12 mm, L/h ≥ 6; taper the prong toward the barb | Taper: Bayer p. 8 (h → h/2, or width → 1/4). Values UNSOURCED — engineering judgment | Bayer URL |
| Prong root fillet | ≥ 0.5 × prong thickness (Hubs); never below 0.38 mm (Bayer) | SOURCED | https://www.hubs.com/knowledge-base/how-design-snap-fit-joints-3d-printing ; Bayer p. 8 |
| Slot width between two prongs | **≥ 2 × barb height + 0.3 mm**, so both prongs can close fully before they touch | Geometry. DERIVED / UNSOURCED value | — |
| Prong width | ≥ 5 mm where space allows (Hubs minimum clip width) | For a small plunger (Ø 5–8 mm), the prong width equals the plunger diameter in Z; accept less and test. SOURCED (Hubs) | https://www.hubs.com/knowledge-base/how-design-snap-fit-joints-3d-printing |
| Plunger-to-bore sliding clearance | **0.2–0.3 mm per side** (0.4–0.6 mm diametral) | Fictiv: 0.4 mm for slide fits (side convention not stated). He 2022 reports (in its limitations discussion) a minimum printing tolerance of 0.6 mm in XY and 0.4 mm in Z at 0.2 mm layers on an Ultimaker. Print-in-place PLA tests: 0.2 mm moves freely (SECONDARY). Chosen range UNSOURCED — engineering judgment | https://fictiv.com/?p=1238 ; He 2022 URL, p. 124 |
| Retention force | With a 90° face, retention is limited by prong shear and buckling, not by friction. Check that the spring's maximum force (rate × max compression) is well below the force to shear the barb | UNSOURCED — engineering judgment | — |
| Mating force (for a lead-in angle check) | W = P·(μ + tan α)/(1 − μ·tan α); friction μ: PC 0.45–0.55, PA 0.30–0.40, PP 0.25–0.30 (no PLA/PETG values given) | Bayer p. 14–15, Table 3. SOURCED | Bayer URL |
| Printed barbed pin examples | No Slant 3D, Thingiverse or Printables barbed plunger with stated dimensions found. Closest: MakerWorld "Snaply" push-button clip with a pen spring (3.2–5.7 mm spring OD), pressed into its casing | SECONDARY | https://makerworld.com/models/2306748 |

### D.1 Geometry that matters more than any number

- **Print orientation decides whether the prongs survive.** Print the plunger lying on its side, with the slot plane perpendicular to the bed. The two prongs then sit left and right of the slot and flex in ±Y, inside each layer. Two other orientations fail. If the plunger prints upright, each prong is a Z cantilever and snaps along a layer line, which is exactly Slant's warning (Slant Snap6 0:40). If the slot plane lies parallel to the bed, the upper prong prints as a bridge and bends across layers.
- **Add a flat to the plunger.** A plunger printed on its side needs a flat face on the bed side for adhesion. A matching flat in the bore keys the plunger, so the prongs always meet the step and cannot rotate into the slot direction (UNSOURCED — engineering judgment).
- **Stack the features in this order along the plunger.** From the outside in: detent tip, sliding body (fits the bore neck), split zone with two prongs, barbs at the inner end. The bore has a narrow neck at the outer face and a wider counterbore inside. The counterbore must be longer than the plunger travel plus the barb length, so the barbs never hit the counterbore floor before the spring goes solid.
- **Seat the spring on the prong tips, not inside the slot.** Choose a spring whose mean diameter falls between the slot width and the plunger diameter, so the end coil bears on both prong tips. The spring then loads the prongs along their axis and cannot enter the slot or block the prongs from closing during insertion. Insert the spring first, then push the plunger in.
- **Check the housing's print orientation too.** If the housing prints with the bore opening facing up, the catch step under the neck is a downward-facing overhang. Do not chamfer it; keep it small or reorient the housing (see the "Catch face as printed" row).
- **Let the shoulder, not the barbs, set the outward stop.** The barbs' 90° faces catch on the inner face of the neck and resist the spring. An outer shoulder or head on the plunger, larger than the neck, stops the plunger from being pushed in too far. With both stops designed, neither the spring nor the user can eject or bury the plunger.

The orientation rule is the single most important design decision for a barbed plunger; the angles and sizes only work after the prongs bend within the layers.

---

## Topic E. G-code pause to capture a spring mid-print

| Parameter | Recommended value | Material / printer notes | Source URL |
|---|---|---|---|
| PrusaSlicer pause | Slice, drag the layer slider, right-click the orange "+", choose "Insert pause print (M601)", enter an LCD message. The pause runs **before** the selected layer prints. Needs PrusaSlicer ≥ 2.2; MK3-family firmware ≥ 3.9.1; not available with sequential printing | SOURCED | https://help.prusa3d.com/article/insert-pause-or-custom-g-code-at-layer_120490 |
| Two heights to name | **Cavity top** = Z of the cavity ceiling in CAD. **Pause layer** = first roof layer, whose top Z shown by the slicer = cavity top + one layer height (h) | Naming convention for the skill. DERIVED | — |
| Which layer to pick in PrusaSlicer | **The pause layer** (slider reading = cavity top + h) | DERIVED from "before the selected layer" | same Prusa URL |
| Pause misplacement report | A user saw a pause set at layer 10 appear at layer 11; re-inserting fixed it | SECONDARY (comment on the Prusa article) | same Prusa URL |
| M600 vs M601 on Prusa | M600 is the colour-change command (filament swap). M601 is a plain pause | SOURCED | https://help.prusa3d.com/article/color-change_1687 |
| Firmware support for M601 | Prusa (MK2/MK3) and Buddy (MINI/MK4/XL/CORE One) support M601. Marlin has no M601: use M125 or M0. Klipper uses PAUSE. RepRapFirmware supports M601 from version 3.01, or M226 | RepRap G-code wiki M601 table. SOURCED | https://reprap.org/wiki/G-code#M601:_Pause_print |
| Marlin M0/M1 | "Pause after the last movement and wait for the user to continue"; ignored without an LCD or EMERGENCY_PARSER; does not itself park | SOURCED | https://marlinfw.org/docs/gcode/M000-M001.html |
| Marlin M600 | Parks, ejects filament, waits, reloads and primes. Do not use it for inserting a spring; it unloads filament | Requires ADVANCED_PAUSE_FEATURE. SOURCED | https://marlinfw.org/docs/gcode/M600.html |
| Cura "Pause at height" | Extensions → Post Processing → Modify G-Code → add "Pause at height". Script settings: "By Layer" = "the number of the LAST layer you want to finish prior to the pause"; "By Height" = pause "at the start of the layer where Z >= [entered value]" | SOURCED (current script; older Cura versions may differ) | https://github.com/Ultimaker/Cura/blob/5bea2f86153faed3a1c2d9081b8d6b753684678a/plugins/PostProcessingPlugin/scripts/PauseAtHeight.py#L126-L149 |
| Which value to enter in Cura | **Use "By Layer" by default** and enter the **last cavity layer** (the layer just below the roof). "By Height" takes **cavity top + one layer height**, but Z-hop moves can falsely trigger height-based pauses (SECONDARY) | DERIVED from the script text | same Cura URL ; https://forum.duet3d.com/post/59698 |
| Cura pause command options | M0 (Marlin), M25 (BQ), M226 (RepRap), @pause (Repetier/OctoPrint), M125, M2000 (Raise3D), PAUSE (Klipper), G4 dwell, custom | SOURCED | Cura URL, lines 154–170 |
| Cura "Reason for Pause" | Choose **"All Others"** for inserts; "Filament Change" adds unload/load/purge | SOURCED | Cura URL, lines 195–199 |
| Cura park and lift | Park the head (default on); "Lift Head Z" default 1.0 mm; "Minimum dist nozzle to plate" default 15 mm | SOURCED | Cura URL, lines 281–364 |
| Ooze compensation after pause | Cura "Extra Prime Amount", default 0.30 mm of filament ("at .2 layer height and .4 line width - 0.10 mm of 1.75 filament … is 3 mm of extrusion"). Keep the nozzle at print temperature through a short pause (Cura "Standby Temperature" setting) | SOURCED | Cura URL, lines 252–257, 370–371 |
| Cura extrusion mode bug | The script was reported to switch relative extrusion to absolute; check the M82/M83 lines | SECONDARY (forum) | https://community.ultimaker.com/topic/35115-a-modest-cura-suggestion-if-you-add-post-processing-script-to-pause-at-height-it-will-change-it-to-relative-extrusion-and-back-to-absolute-extrusion-even-if-you-have-relative-extrusion-set-in-the-global-slicer-settings/ |
| Bambu Studio pause | Preview tab → layer slider → right-click "+" → "Add Pause"; re-slice. The pause G-code is `M400 U1` in the printer profile | SECONDARY (community forum; no official Bambu page found) | https://forum.bambulab.com/t/how-to-change-the-default-pause-settings/147603 ; https://forum.bambulab.com/t/bambu-studio-adds-a-color-change-when-pause-added/12732 |
| Bambu caveats | Pause can show as a colour-change marker; some users report pauses lost on project save; Bambu Handy cannot program pauses | SECONDARY | same Bambu forum URLs |
| Cavity top Z in CAD | **Snap the cavity top to a layer boundary**: cavity top = first-layer height + n × layer height | Mid-layer slicing otherwise trims or extends the cavity by up to one layer, silently. DERIVED from PrusaSlicer `slice_z` | https://github.com/prusa3d/PrusaSlicer/blob/30ef59195e0f3ee6f270b185bb5f9fb5f349f81f/src/libslic3r/src/libslic3r/PrintObjectSlice.cpp#L62 |
| Head-room under the roof (collision and sag) | Spring top and any captured cap must sit **0.3–0.5 mm below the cavity top**. The margin keeps the nozzle clear when the pause layer prints and leaves room for a drooping first bridge layer, which Slant warns "can make the latch jam" | Prusa warns inserted magnets must sit firmly in their slots or they "get stuck to the print head as it passes over them". Margin UNSOURCED — engineering judgment | https://help.prusa3d.com/article/insert-pause-or-custom-g-code-at-layer_120490 ; https://www.youtube.com/watch?v=IZKh6lo9SP4&t=285 |
| Cavity height, spring captured free | Spring free length + the 0.3–0.5 mm head-room (+ free-length tolerance, e.g., ±0.46 mm on LC 016A 05 S) | Lee lists free-length tolerance per part. Margin UNSOURCED — engineering judgment | https://www.leespring.com/product/compression-spring-lc016a05s-stainless-steel |
| Spring captured compressed | Do not let a compressed spring push on a bridge roof while it prints; it will lift the roof. Instead, drop in the spring plus a printed cap or plunger that is held by a feature already printed (a lip, or a twist-lock), or capture it free and let a later-inserted plunger compress it | UNSOURCED — engineering judgment | — |
| Cavity diameter | Spring OD + 0.35–0.6 mm diametral (Topic C rule) | DERIVED | see Topic C |
| Roof over the cavity | Keep the span short: bridges under ~5 mm show no sag; longer spans sag | Hubs. Qidi says ~20 mm clean on a tuned printer (SECONDARY). Spring bores of 3–8 mm are within or near the 5 mm sag-free span. SOURCED (Hubs) | https://www.hubs.com/knowledge-base/how-design-parts-fdm-3d-printing/ |
| Roof alternatives | Use a captured printed cap dropped in at the pause, or a 45° chamfered/teardrop roof for wider cavities | Slant Snap6: replace flat overhangs with 45° chamfers (5:02). SOURCED (principle) | https://www.youtube.com/watch?v=rsfZgT3ZEI8&t=302 |
| Verification step | Export G-code, find the pause command (M601 / M0 / M125 / PAUSE / M400 U1), and confirm that the next layer Z after it equals cavity top + one layer height | UNSOURCED — engineering judgment (procedure) | — |

### E.1 How the skill should document a pause

The question is "what must a reader of the design know to print it?" The skill should record four facts in the design notes, in this order.

1. **Cavity top Z** (for example "Z = 8.20 mm"), snapped to a layer boundary for the stated first-layer and layer heights.
2. **Pause layer per slicer** (pause layer = cavity top + h): PrusaSlicer and Bambu Studio select the layer at Z = 8.40 mm (the first roof layer, at 0.2 mm layers); Cura "By Layer" (preferred) enters the last cavity layer number; Cura "By Height" enters 8.40.
3. **Pause command per firmware**: M601 on Prusa, M0 or M125 on Marlin, PAUSE on Klipper, M400 U1 on Bambu. Never M600 for an insert on Marlin.
4. **Insert instruction for the LCD message**, for example "Drop spring LC 018B 05 S, then plunger, flat side down. Resume."

The pause layer is always the first layer that closes the cavity, and the cavity top must sit exactly on a layer boundary one layer below it.

---

## Open items the skill author should test, not trust

- Fin interference (0.2–0.3 mm per side) and fin length (≥ 9.5–10.5 mm) are engineering judgment, cross-checked only by strain arithmetic and the video 1 readout.
- Printed-bore allowance over Lee's hole value (+0.2–0.3 mm) varies by printer and material. A one-off test bore settles it.
- PrusaSlicer "thick bridges" behaviour over a one-layer relief gap is unverified.
- No primary source gives printed-flexure fatigue cycle counts. The low-strain rules are the only defence.
- No primary source gives yield strain for printed nylon, PP or TPU. Hubs only names them as strain-resistant.
