# Joint for a 400 mm bracket in 3 sections (PLA, mixed printers)

## Mechanism and why
The question is which sliding joint lets three sections register and stay put without glue on printers that each fit differently. Use the **eye slot with grip fins** (Slant 3D joint B5), two joints in total (section 1 to 2, section 2 to 3). A round "eye" tongue slides into a round pocket lined with thin, tangentially leaning fins. The fins bend to grip and centre the tongue, so printer-to-printer size differences are absorbed by fin flex instead of by a tuned clearance. The fit is set by one circle, and the curved first layer resists warping. Each section is about 133 mm, well inside a 250 mm bed.

The plain square tongue, and the rigid T-slot, are tolerance-sensitive and are not recommended for mixed printers. The flexible T-slot is the default sliding joint, but its flanges stay preloaded and PLA relaxes. The eye with grip fins is the better choice here because it is explicitly the mixed-printer variant.

## Parameters (0.4 mm nozzle, 0.2 mm layers, PLA)
| Parameter | Value | Tag |
|---|---|---|
| Eye tongue diameter | 20 mm (scale to about 60% of the bracket section height if the arm is thinner) | `[video]` Ø20 in a 25 mm block |
| Neck width | about 5 mm | `[measured estimate]` |
| Neck clearance per side | 0.2-0.3 mm | `[source: UF Marston Makerspace]` |
| Fin thickness | 0.45 mm (soft) or 0.9 mm (firm). Never 0.1-0.34 mm, because Arachne widens it | `[source: Prusa KB]` |
| Fin count | about 15 on a Ø20 eye (range 8-16, tips at least 3 mm apart) | `[measured estimate; range judgment]` |
| Fin lean | 30-45 degrees from radial | `[measured estimate]` |
| Radial interference per fin | 0.3-0.5 mm | `[judgment]` |
| Fin free length (PLA, t = 0.45) | 6.3-8.2 mm (about 7.3 mm for 0.4 mm deflection at 0.5% sustained strain) | `[derived]` |
| Gap from fins to roof and floor | at least 0.4 mm, 0.6 mm safer | `[judgment]` |
| Leading-edge chamfer on fins | 45 degrees, about half the fin length | `[video; size judgment]` |
| Chamfer on tongue tip and pocket mouth | 45 degrees x 0.5-1.0 mm | `[video; size judgment]` |
| Lengthwise taper | 1-2 degrees, so the slide starts loose and ends tight | `[source: Siraya]` |
| Bed-edge chamfer, elephant-foot compensation | 45 degrees x 0.4-0.6 mm, EFC about 0.2 mm | `[video; source: Prusa KB]` |
| Vertical corner radius | R 2 mm or more | `[measured]` |

Flag: every `[judgment]` and `[estimate]` value (interference, fin count, lean, roof gap) needs one test print before you commit three sections to it.

## PLA caveat
PLA creeps. Sustained strain must stay at or below 0.5%, which is why the fins above are long and thin (6-8 mm at 0.45 mm). A PLA fin that stays bent for a day will not fully spring back, so grip will loosen over weeks. If you can print the female half (the fin pocket) in PETG, do that, since PETG allows 1.0% sustained strain and shorter fins (4.5-5.8 mm). Otherwise accept PLA and plan to re-seat or glue-free retighten by swapping a section.

## Print orientation
- Print each eye tongue and each fin pocket with the eye circle flat to the bed, so the fins and the circle lie in the XY plane and extrude in Z. Bending then runs along deposited lines, not across layer interfaces.
- Orient the sections so the slide axis is along the printed part length where possible, with a plain filleted-square footprint on the bed.
- No supports: the fin underside is a flat layer, and the roof relief is bridged at 0.4-0.6 mm.

## CAD steps
1. Sketch the eye pocket circle on the mating face, plus the slot to the edge for the neck.
2. Model one fin as a thin body (0.45 mm), leaning 30-45 degrees tangentially, with free length 6.3-8.2 mm, tip chamfered at 45 degrees.
3. Circular-pattern about 15 fins around the eye.
4. Cut roof and floor relief so the fins are detached by 0.4-0.6 mm (cantilevers, not fused).
5. On the tongue part, model the Ø20 circle on a 5 mm neck with 0.2-0.3 mm per side neck clearance, oversized to produce the 0.3-0.5 mm per-fin interference.
6. Add the 1-2 degree lengthwise taper, 45 degree chamfers, and R 2 mm vertical corners.
7. Add the bed chamfer and EFC.

## Tuning
- Too loose or jiggles: raise interference toward 0.5 mm, or move fins from 0.45 to 0.9 mm.
- Too hard to insert: lower interference, thin fins, or add taper.
- Fins fused to roof or floor: the gap is too small, so use 0.6 mm.
- Do not adjust slicer settings to make it fit. If you need to, the geometry is wrong.

## Honest limit for a shelf bracket
Friction fins resist pull-apart and side slop, but a bracket carries bending load, and a joint at mid-span sees that moment. Place the joints where bending moment is lowest where you can (not at the wall corner), keep the eye diameter large relative to arm height, and expect the joint to be the weak point. If the shelf is heavy, add the bi-directional locking tab (Slant's tool-free snap-in, `snap-fits.md`) or a printed or metal pin through the joint rather than relying on fin friction alone. Test with real load before use.
