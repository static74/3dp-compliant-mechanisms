# Joint for a 400 mm PLA shelf bracket in 3 sections

## Recommendation
Use an **eye slot with grip fins** (Slant's B5 joint) to centre and carry each section, plus a **bi-directional locking tab** (B6) in the slide direction to stop it backing out. Each of the two joints gets one fin-lined eye and one flat key rib so it cannot rotate.

Why: the sections come from different printers, so any joint whose fit depends on a clearance will drift. The fin eye grips an oversize tongue and self-centres, so the same file works on any printer. A plain tongue or T-slot is tolerance-sensitive. The flexible T-slot relies on preloaded flanges, which relax in PLA. In this design the locking-tab arm is relaxed once seated, so PLA creep does not release it. The fins are the only preloaded parts, and they are held to the PLA sustained-strain limit.

Sections are about 133 mm each, so they fit the 250 mm bed with margin. A shelf bracket carries bending, and none of the tongue-and-slot joints is sized for it on its own. That is why the design adds a key rib, a long engagement and a positive stop.

## Assumptions to confirm
- Section depth (the dimension the joint spans) is at least 45 mm, and thickness along the eye axis is at least 10 mm. The fin pocket needs about 44 mm across. If your bracket is slimmer, tell me the section and I will rescale.
- Slide direction is across the bracket thickness, not along the load. Gravity then acts across the slide axis, and the joint cannot slide apart under shelf load.
- Load and allowable deflection are unknown. Engagement length is set by the rule below; check it against your real load with one test piece.

## Parameters (0.4 mm nozzle, 0.2 mm layers, PLA)
| Parameter | Value | Tag |
|---|---|---|
| Eye tongue diameter | 20 mm | `[video, on screen]` |
| Neck width | about 5 mm, clearance 0.2-0.3 mm per side | `[measured estimate]` / `[source: UF]` |
| Fin thickness | 0.45 mm (soft; never 0.1-0.34 mm) | `[source: Prusa KB, Arachne]` |
| Fin count | 15 (tips about 4 mm apart at r 9.7; must be at least 3 mm) | `[measured estimate]` |
| Fin lean | 45 degrees from radial | `[measured estimate]` |
| Radial interference per fin | 0.3 mm | `[judgment]` |
| Unloaded fin tip radius | 9.7 mm (tongue radius 10 minus 0.3) | `[derived]` |
| Fin free length L | 8 mm. Minimum for PLA at 0.5 % is 7.5 mm for 0.3 mm interference at 45 degrees; strain = 1.5 x 0.424 x 0.45 / 8^2 = 0.45 % | `[derived]` |
| Gap from fins to roof and floor | 0.6 mm | `[judgment]` |
| Fin leading-edge chamfer | 45 degrees, about 4 mm long | `[video; size judgment]` |
| Pocket envelope | fin root radius 16.4 mm, so pocket body about Ø40 and part at least 44 mm across | `[derived]` |
| Key rib (anti-rotation) | flat tongue, about 8 mm wide, 0.25 mm per side, 1-2 degree lengthwise taper | `[source: UF, Siraya]` / `[judgment]` |
| Engagement length | at least 1.5 x section height | `[judgment]` |
| Locking tab flange | root 1.8 mm tapering to 0.9 mm, width 6 mm, length 10.5 mm, bump 0.8 mm | `[source: Bayer; Hubs]` |
| Tab angles | insertion 30 degrees, return 45 degrees (releasable) or 63-90 degrees (permanent) | `[source: Bayer, BASF]` |
| Tab strain | 1.2 % repeated snap, PLA | `[derived]` |
| Tab mating gap | 0.25 mm per side | `[source: Fictiv, Qidi]` |
| Corner radii on the bed face | R 2 mm or more, filleted square footprint | `[video]` |

Fins at 0.5 % are at the PLA sustained-preload ceiling `[judgment]`, so expect some force loss over weeks. The tab and the key rib carry the retention, not the fins.

Flag as needing one test print: interference (0.3 mm), fin count, fin lean, key rib width and taper, and engagement length. Every `[judgment]` value above is untested on a printer.

## Orientation
Print each section with the eye axis vertical, so the circular profile lies on the bed. Fins and tab flanges then bend in XY along deposited lines, not across layer interfaces. Chamfer all bed edges 45 degrees by 0.4-0.6 mm, except the fin bottoms (thin footprint): leave those square and keep at least 0.8 mm of flat. Underside of tab flanges at 45 degrees or less from vertical so no supports are needed. Use 3 or more perimeters and elephant-foot compensation of about 0.2 mm. Set a 0.6 mm relief gap above and below the fins so they print detached.

## CAD steps
1. Split the bracket into three sections at about 133 mm. Make the middle section carry a tongue at each end, and the end sections each carry the matching eye pocket (or use the reverse; keep one convention).
2. On the eye face, sketch a Ø20 circle and a 5 mm neck slot to the edge. Add the key rib beside it, tapered 1-2 degrees.
3. Model one fin as a thin 0.45 mm body, leaning 45 degrees, 8 mm long, root at radius 16.4 mm, tip at 9.7 mm. Chamfer its leading edge, then circular-pattern 15 copies.
4. Cut the 0.6 mm roof and floor relief so the fins cantilever.
5. Add the locking tab: 10 x 10 mm stem with two flanges on opposite faces, bump 0.8 mm, plus the matching V recesses in the cavity. Chamfer flange undersides to 45 degrees or less.
6. Fillet all inside corners (rolling ball) and round vertical corners to R 2 mm or more.

## Tuning
- Joint rattles: raise interference in 0.1 mm steps or thicken fins to 0.9 mm, then recheck strain.
- Too hard to slide in: lower interference to 0.2 mm or lengthen the fins.
- Fins feel loose after a week: expected PLA creep. Reprint in PETG if the joint must stay tight, or rely on the tab.
- Tab will not click: deepen the bump, or lower the insertion angle to 20-25 degrees.
- Tab breaks at the root: add the 1.1 mm root fillet or lengthen the arm.
- Run all three sections on at least two different printers before committing to the final set. That is the real test of the design.
