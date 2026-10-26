# Compliant lids: press-fit, perforated plug, side springs, grip fins, spring latches

**Family:** compliant-lid (a plug lid that fits a separately printed box on any printer)
**Use when:** a lid, cap, plug or insert must fit an opening without tuning clearance per material or machine.
**Avoid when:** the lid must seal (fins and springs leave gaps) or the box wall is under 2 mm (fins need something to press against).
**Source:** Slant 3D "Design Compliant Lids for Perfect Tolerance Every Time" (Lids Vol. 2). All geometry is measured from frames against the stated 85 mm footprint unless tagged otherwise.

## Reference part `[video 85 mm; rest measured]`
Box 85 × 85 × ~26 mm, walls ~5 mm, R5 vertical corners. Lid = flange 85 × 85 × ~6 mm with the plug 75 × 75 × ~8 mm on top (5 mm step per side, R5 corners), printed flange-down. 45° chamfer on both bed-side edge loops, ~2 mm fillet band on the plug top edge, 0.2 mm layers (inferred).

## Progression and when to pick each `[video]`
| Lid | Fit character | Pick it when |
|---|---|---|
| A. Press-fit | friction on the whole wall; permanent if solid | glued or never-removed closures |
| B. Perforated plug | reduced contact, tighter yet loose; down to a single nub = easy open | friction lid that must open easily |
| C. Side springs | two in-plane cantilevers with nubs, ~universal fit | removable lid, moderate retention |
| D. Grip fins | 35 fins per side, redundant, tight but removable | the default removable lid |
| E. Spring latches | ~2 mm travel, positive detent | lids that must click and hold against a load |

## A. Press-fit `[video]`
Round all edges, chamfer the first layer against elephant foot, and accept it as permanent. Problem: too much wall contact, so any deviation fights a large area.

## B. Perforated plug `[measured]`
| Parameter | Value | ± |
|---|---|---|
| Pocket | Ø10 mm cylinder, centred 2 mm inside the plug wall (opening at the wall ≈ 9.2 mm, depth into plug ≈ 7.2 mm) | derived from "5 edges 157.08 mm" readout, exact |
| Count | 5 per side, 20 total, none at corners | exact |
| Pitch | 13.5 mm; first hole ≈ 5.5 mm from the corner | 0.3 |
| Depth | full plug height, stopping at the flange top | inferred |
Variants `[video]`: fewer, larger pockets down to a single contact nub per side for an easy-open lid; solid for permanent.
Model: circle on the plug top face centred on the edge, linear-pattern 5, circular-pattern ×4, extrude-cut down the plug.

## C. Side springs `[video + measured]`
Two cantilever arms cut out of one plug wall, flexing in the XY plane (never vertical across layers: "they push out and snap along the layer lines" `[video]`), each with a small nub that presses into the box wall or into a dimple.
| Parameter | Value | Tag |
|---|---|---|
| Arm length × thickness | 22.5 × 2.5 mm (sketch typed 25 × 5, then edited to 22.5074 × 2.5) | `[video on screen]` |
| Slot behind arm | 2.5 mm; free-end gap 2.5 mm; arm fixed at one end (cantilever) | `[measured ±0.3]` |
| Arms | 2, on one wall, ~14.6 mm apart, centred; add to all four walls for even retention `[judgment]` | `[measured]` |
| Corner fillets | R1 | `[video on screen]` |
| Nub | Ø1.6–2 mm dome, 0.3–0.5 mm proud, ~75 % along the arm from the root | `[measured ±0.5]` |
| Bottom relief | 0.3 mm slab removed under the arm so it floats above the flange (video modelled 0.2; 0.3 survives any layer height) | `[video + second Slant video]` |
Strain check: PLA, t 2.5, L 22.5, y 0.5 → ε = 1.5·y·t/L² = 0.37 %, well inside sustained limits. Tune: thicker arm = tighter, thinner = looser `[video]`.
Model: rectangle 22.5 × 2.5 along the wall on the plug top face, mirror for the second arm, extrude-cut the slot, fillet R1, extrude a small boss for the nub, cut the 0.2 mm relief under the arm.

## D. Grip fins `[video + measured]` (the default removable lid)
Take the side-spring idea around the whole perimeter: dozens of thin slanted blades make the plug's effective perimeter slightly larger than the opening, each one a tiny in-plane cantilever. Redundant, so one broken fin does not matter.
| Parameter | Value | Tag |
|---|---|---|
| Slit width | 0.5 mm | `[video on screen]` |
| Slits per side / fins per side | 35 / 36 | derived from "140 edges 538.12 mm", exact |
| Pitch | 1.9 mm | `[measured ±0.1]` |
| Fin thickness | 1.4 mm along the wall, 1.27 mm perpendicular to the slit (3 perimeters) | `[measured ±0.15]` |
| Slit angle | 24.6° from the wall normal (≈65° to the wall) | `[measured ±3°]` |
| Slit length | 7.19 mm; depth into plug ≈ 5.0 mm plus 1.55 mm of sketch beyond the wall | derived, ±0.05 |
| Fin free height | ≈ 7 mm (the plug height less the relief) | `[measured ±1.5]` |
| Bottom relief | **0.3 mm** (0.3 min, 0.5 max). Video 1 modelled 0.2 and said 0.3; Slant's tolerance video settles it at 0.3 because slicers cut each layer at mid-height, so a gap under one layer can vanish at 0.25–0.3 mm layers. Use 0.4–0.5 with a 0.6 mm nozzle | `[video XKrDUnZCmQQ 5:27; source: PrusaSlicer slice_z]` |
| Interference | not visible in frames (fin faces look flush with the corner blocks); 0.2–0.3 mm per side; 0.5 only for PETG lids opened often `[judgment]` | |
| Corners | solid R5 blocks, no fins through the arc | `[measured]` |
| Fin top | rounded 0.5–1 mm lead-in | `[measured]` |
Two fin recipes. **As Slant modelled it** `[measured]`: 1.27 mm fins, 1.9 mm pitch, 7.2 mm slits, 65° to the wall. **Strain-safe default** `[derived, held strain ≤ 0.5 %]`: fins 0.86 mm (two perimeters at the slicer's thin-wall width), pitch 2.5–3 mm, length ≥ 10.5 mm at 45° or ≥ 9.5 mm at 30° for 0.3 mm interference, 30–45° from the wall. Slant's thicker, shorter fins run near 0.6–2 % strain and rely on the load being shared by many fins; Slant says they "deflect so little" they do not creep. Offer the measured recipe when the user wants Slant's part, the strain-safe one for PLA lids that stay closed. A radial (90°) fin cannot bend and only buckles; the slant converts radial interference into bending `[derived]`.
Tune `[video]`: longer fins = softer; thicker = firmer, like any spring.
Model: sketch one slanted 0.5 mm parallelogram on the plug top face along one edge, linear-pattern 35 at 1.9 mm (or ~26 at 2.5 mm for the strain-safe recipe), circular-pattern ×4 skipping corners, extrude-cut down the plug wall, cut a 0.3 mm slab at the fin bases, fillet fin tops. Keep a rigid locating base below the fins: Slant's pattern is a square rigid plug that aligns the lid, with compliance above it `[video]`. Export STL at fine tessellation and check the 0.3 mm gap survived; Slant saw exporters close it `[video]`.

## E. Internal spring latches `[video; geometry mostly judgment]`
Small latch blocks in windows on two opposite plug walls, pushed outward by a spring inside the lid, dropping into detents in the box; ~2 mm of travel `[video]`. Harder to design: the roof over the latch cavity can sag and jam the latch `[video]`.
| Parameter | Value | Tag |
|---|---|---|
| Window in plug wall | ≈ 7.9 × 5.4 mm, centred, bottom at the flange top | `[measured ±0.8]` |
| Latch block | ≈ 6.9 mm wide, 0.3–0.5 mm gap on three sides | `[measured ±0.8]` |
| Travel | ~2 mm | `[video]` |
| Protrusion at rest | 0.5–1.0 mm beyond the plug wall | `[judgment]` |
| Latch nose | 30° insertion ramp, 45° release ramp (releasable) | `[source: Bayer]` |
| Box detent | pocket 1.0–1.5 mm deep, width = latch + 0.6 mm, same ramps | `[judgment]` |
| Cavity roof | chamfer to 45° or keep the bridge ≤ 5 mm; add a 0.5 mm Z gap over the latch | `[source: Hubs; judgment]` |
| Release | a 2 × 2 mm slot in the flange face above each latch for a hook tool | `[video shows tool; size judgment]` |
Spring: the video never shows it. Use spring-loaded.md: a printed serpentine or cantilever leaf in the XY plane behind the latch (default), or a metal compression spring captured per spring-capture.md. The latch is the plunger in that file.

## Print (all lids)
Flange down. Fins, arms and latches all have their profile in XY. Any layer height ≤ 0.3 mm with the 0.3 mm relief. 3 perimeters. No supports. Keep the slicer's "detect thin walls"/Arachne defaults; fin thickness is already a whole perimeter multiple.

## Failure modes
- Fins or arms fused to the flange: relief gap under one layer height, or the STL exporter closed it; use 0.3 mm and check the mesh.
- Arm snapped: built vertically or too thick; keep in-plane, ≤ 2.5 mm thick, R1 fillets.
- Lid loosens over weeks (PLA): creep; PETG/ASA or thinner, longer fins.
- Latch jams: roof sag; chamfer or shorten the bridge, add Z gap.
- Corner of fin set has flash: the video trims it with a knife; chamfer the corner block top.
