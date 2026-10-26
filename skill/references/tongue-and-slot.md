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
| Flange arc | circle ≈ 1.6–2× the neck width, trimmed; radius ≈ 1–1.5× the T half-width | `[measured estimate]` |
| Preload at each flange tip | 0.3–0.5 mm | `[judgment]` |
| Flange free length | from y = 0.67·ε·L²/t at sustained ε: PETG t 0.9, y 0.4 → L ≥ 7.3 mm | `[derived]` |
| Slot tilt | 20–30° off the bed normal | `[measured estimate]` |
| Neck clearance | 0.2–0.3 mm per side; only the springs locate | `[source: UF]` |
Material: the flanges stay preloaded, so PETG, ASA or nylon. PLA relaxes.

## Eye slot (B4) `[video]`
Circular tongue (Ø20 mm in a 25 mm block `[video, on screen]`) on a neck (~5 mm wide `[measured estimate]`). One circle dimension controls the fit; curved first layer resists warp. Clearance 0.2 mm per side on the eye, 0.2–0.3 on the neck. Short, stumpy slots spread at the top like a clamshell: deepen the slot at the cost of insertion force.

## Eye slot with grip fins (B5) `[video]`
Line the circular pocket with thin fins, detached from the roof and floor so they cantilever, leaning tangentially like iris blades; push in a slightly oversize eye tongue and the fins grip and centre it. Impossible to mould or machine; a printing-only feature. Thicker or longer fins grip harder.
| Parameter | Default | Tag |
|---|---|---|
| Fin thickness | 0.45 mm (soft) or 0.9 mm (firm); never 0.1–0.34 | `[source: Prusa KB, Arachne]` |
| Fin count | ~15 on a Ø20 eye; 8–16, tips ≥ 3 mm apart | `[measured estimate; range judgment]` |
| Lean | 30–45° from radial | `[measured estimate]` |
| Radial interference per fin | 0.3–0.5 mm | `[judgment]` |
| Free length | PETG t 0.45: 4.5–5.8 mm; PLA t 0.45: 6.3–8.2 mm (sustained strain) | `[derived]` |
| Gap to roof/floor | ≥ 0.4 mm (2 layers), 0.6 safer | `[judgment]` |
| Leading-edge chamfer | 45°, about half the fin length (video uses two-distance chamfer) | `[video; size judgment]` |
Model: circle on the face, slot to the edge for the neck, one fin as a thin body, chamfer it, circular-pattern around the eye, then cut the roof/floor relief.

## Model it (flexible T)
1. Sketch the slot profile on the mating face: neck rectangle plus a crossbar.
2. On the tongue part, sketch a circle centred on the neck axis, diameter 1.6–2× neck width; trim it to the two outer arcs that become flanges; keep flange thickness 0.9–1.35 mm.
3. Extrude tongue and slot; slot offset per the clearance table; flanges oversize by the preload.
4. In the bottom view, sketch the tilt and cut so the slot enters the part at 20–30°.
5. Fillet the slot corners (rolling-ball), chamfer flange edges and tongue tip at 45°.

## Tune it
Jiggles: raise preload or thin the flange to lengthen L. Hard to slide: lower preload, add 1–2° taper. Spreads at the top: deepen the slot or add a cross-bar. Warps: simplify the first layer by tilting the slot or switching to the eye.

## Failure modes
- T-bar first layer curls (ABS/ASA): tilt the slot or use the eye.
- Flanges relax in PLA: PETG, or accept it as a one-time assembly.
- Fins fused to roof: relief gap too small; use ≥ 2 layers.
