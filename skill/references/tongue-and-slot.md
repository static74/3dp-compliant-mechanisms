# Tongue-and-slot family: tongue, T-slot, flexible T-slot, eye slot, grip-fin eye slot, dovetail

**Family:** sliding joints between separately printed parts
**Use when:** two panels or blocks must register edge-to-edge and resist pull-apart, especially large assemblies printed in sections.
**Avoid when:** a plain square tongue is all you can fit; it is tolerance-sensitive and weak `[video]`. Prefer the eye slot or the flexible T.
**Source:** Slant 3D joints guide Part B.

## Progression and when to pick each `[video]`
| Joint | Verdict | Pick it when |
|---|---|---|
| Square tongue (B1) | weak, many tolerances | never, except as a glued key |
| T-slot (B2) | lateral support, cannot pull apart, but three tolerances and a complex first layer that warps | rigid parts, low-warp material |
| Flexible T-slot (B3) | curved flanges act as leaf springs: no jiggle, shrinkage-tolerant | the default sliding joint |
| Eye slot (B4) | one circle sets the fit, simple curved first layer | tongue must print face-down, or you want a pivot |
| Eye slot with grip fins (B5) | fins centre and grip an oversize tongue | parts from different printers or materials must fit |
| Locking tab (B6) | see snap-fits.md | tool-free assembly kits |

## Shared geometry
| Parameter | Default | Tag |
|---|---|---|
| Sliding clearance | 0.20–0.30 mm per side (ABS/ASA at the top) | `[source: Qidi, UF]` |
| Chamfer on tongue tip and slot mouth | 45° × 0.5–1.0 mm; it wedges and locks layer lines | `[video; size judgment]` |
| Lengthwise taper | 1–2° so the slide starts loose and ends tight | `[source: Siraya]` |
| Internal slot corners | dog-bone or circular reliefs; FDM cannot print sharp inside corners | `[source: UF]` |
| Dovetail flank | 15° per side (10–20°); overhanging face ≤ 45° when the slot prints open-side-up | `[judgment]` |
| First layer | EFC 0.2 mm + 45° bed-edge chamfer; angle the slot so the footprint is a plain filleted square | `[video + source: Prusa KB]` |

## Flexible T-slot (B3) `[video]`
Take a T tongue and curve the two outer flanges into arcs so they act as leaf springs instead of rigid friction pads. Angle the slot through the part so the first layer is a filleted square and the complexity happens higher up; chamfer the flange edges. Downside: an open slot in the bottom face.
| Parameter | Default | Tag |
|---|---|---|
| Flange thickness | 0.9–1.35 mm (2–3 perimeters) | `[judgment]` |
| Flange geometry | name the neck width n and the bar width W (Slant's proportion is W ≈ 2–2.5 n `[measured estimate]`; size W from strain, below). Each flange is an arc centred on the neck axis in the bar's base plane, radius R = W/2 (so the arc ends at the bar tip), starting where it clears the neck (angle asin(n/2R) from the base plane) and ending at 90°. Load is radial at the tip. Bending span L = arc length = R·(π/2 − asin(n/2R)). Worked: n 5, W 14 → R 7, L = 7·(1.571 − 0.365) = 8.4 mm | `[derived from frames; judgment]` |
| Preload at each flange tip | 0.3–0.5 mm | `[judgment]` |
| Flange free length | from y = 0.67·ε·L²/t at sustained ε: PETG t 0.9, y 0.4 → L ≥ 7.3 mm, satisfied by the W 14 example (L 8.4, ε = 1.5·0.4·0.9/8.4² = 0.77 %). W 12 gives L 6.9 and 1.15 %, too high for PETG, so W = 2.8 n is the floor for n 5 | `[derived]` |
| Slot tilt | default: no tilt, slide axis in Z, flanges flexing in XY, slot open on the bottom face (the T outline is then part of the first layer; acceptable in PLA/PETG). Slant tilts the slot 20–30° about the horizontal axis along the T bar so the first layer is a plain square for warp-prone ABS/ASA `[video]`; that puts a sin(tilt) fraction of the bending strain across layers and is not qualified here. If you must tilt, stay ≤ 20° and test | `[video; limit judgment]` |
| Neck clearance | 0.2–0.3 mm per side; only the springs locate | `[source: UF]` |
Material: the flanges stay preloaded, so PETG, ASA or nylon. PLA relaxes.

## Eye slot (B4) `[video]`
Circular tongue (Ø20 mm in a 25 mm block `[video, on screen]`) on a neck (~5 mm wide `[measured estimate]`). One circle dimension controls the fit; curved first layer resists warp. Clearance 0.2 mm per side on the eye, 0.2–0.3 on the neck. Short, stumpy slots spread at the top like a clamshell: deepen the slot at the cost of insertion force.

## Eye slot with grip fins (B5) `[video]`
Line the circular pocket with thin fins, detached from the roof and floor so they cantilever, leaning tangentially like iris blades; push in a slightly oversize eye tongue and the fins grip and centre it. Impossible to mould or machine; a printing-only feature. Slant says thicker or longer fins grip harder `[video]`; the physics is that thicker fins are stiffer and longer fins are softer at equal interference, so lengthen fins to cut strain and creep, thicken them or raise interference to grip harder.
| Parameter | Default | Tag |
|---|---|---|
| Fin thickness | 0.45 mm (soft) or 0.9 mm (firm); never 0.1–0.34 | `[source: Prusa KB, Arachne]` |
| Fin count | ~15 on a Ø20 eye; 8–16, tips ≥ 3 mm apart | `[measured estimate; range judgment]` |
| Lean | 30–45° from radial | `[measured estimate]` |
| Radial interference per fin | 0.3–0.5 mm | `[judgment]` |
| Free length L | a fin leaning θ from radial must bend y = δ/sin θ to absorb radial interference δ (the tip slides on the tongue). L = √(1.5·t·(δ/sin θ)/ε_sustained). At θ 45°, t 0.45: PLA (0.5 %) 7.5–9.8 mm for δ 0.3–0.5; PETG (1 %) 5.3–6.9 mm. At t 0.9 multiply by 1.41 | `[derived]` |
| Gap to roof/floor | ≥ 0.4 mm (2 layers), 0.6 safer | `[judgment]` |
| Leading-edge chamfer | 45°, about half the fin length (video uses two-distance chamfer) | `[video; size judgment]` |
Pocket envelope: the fins are female and face inward, so the **unloaded** tip radius is r = tongue radius − interference (a Ø20 tongue at δ 0.4 has tips at r 9.6); the tongue then pushes the tips outward to r 10 when inserted. With θ measured from radial at the tip, a straight fin of length L has its root at radius √(r² + L² + 2·r·L·cos θ); add fin thickness, a 1 mm root land and ≥ 1.8 mm of wall. For r 9.6, L 8, θ 45°: root radius 16.3 mm, so the pocket body is about Ø37 and the part ≥ 41 mm across the joint `[derived]`.
Model: circle on the face, slot to the edge for the neck, one fin as a thin body, chamfer it, circular-pattern around the eye, then cut the roof/floor relief.

## Structural joints (brackets, spans, anything that carries bending)
Every joint above locates and resists pull-out; none is sized for bending. For a load-bearing section joint add: engagement length ≥ 1.5 × the section height; two eyes or an eye plus a flat tongue so the joint cannot rotate about the eye; a positive stop against slide-out (locking tab from snap-fits.md, or a cross pin); and state the load, section and allowable deflection before choosing dimensions `[judgment]`.

## Model it (flexible T)
1. Sketch the slot profile on the mating face: neck rectangle plus a crossbar.
2. On the tongue part, set n and W (W ≥ 2.8 n for PETG at 0.4 mm preload; recheck strain for other values). Sketch a circle of radius R = W/2 centred on the neck axis in the bar's base plane; keep only the two arcs from asin(n/2R) to 90° on each side; offset them inward by the flange thickness (0.9–1.35 mm) to make the flange profiles.
3. Extrude tongue and slot; slot offset per the clearance table; flanges oversize by the preload.
4. Default: no tilt; the slot runs along Z and exits the bottom face. Only for warp-prone ABS/ASA, and only if you accept an unqualified cross-layer strain component, tilt the slot ≤ 20° about the horizontal axis along the T bar and test it.
5. Fillet the slot corners (rolling-ball), chamfer flange edges and tongue tip at 45°.

## Tune it
Jiggles (low contact force): raise preload, or thicken the flange at the same L; then recheck strain. Too much strain: lengthen L (bigger W) at the same preload. Hard to slide: lower preload, add 1–2° taper. Interference, thickness and length are independent knobs; change one and recompute both force and strain. Spreads at the top: deepen the slot or add a cross-bar. Warps: simplify the first layer by tilting the slot or switching to the eye.

## Failure modes
- T-bar first layer curls (ABS/ASA): tilt the slot or use the eye.
- Flanges relax in PLA: PETG, or accept it as a one-time assembly.
- Fins fused to roof: relief gap too small; use ≥ 2 layers.
