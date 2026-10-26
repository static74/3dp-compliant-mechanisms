# Glue-assist features

**Family:** glue-assist (bonded assemblies)
**Use when:** parts will be glued and you want the bond to key mechanically, excess glue to have somewhere to go, or glue to be injected after assembly.
**Source:** Slant 3D joints guide Part C; Henkel/Loctite plastics bonding guide.

## Features `[video]`
| Feature | Geometry | Tag |
|---|---|---|
| Undercut pocket grid (C1) | small square pockets cut 0.5 mm deep with a taper so each widens with depth; ~15 × 15 grid on a pad; glue keys into the undercut and excess glue has a place to go, preserving the stated dimension | `[video −0.5 mm; count measured]` |
| Pocket opening | ≥ 0.9 mm so the slicer keeps it open; pitch 2–3 mm; taper 10–20° per wall, every widening wall ≤ 45° from vertical | `[judgment]` |
| Directed glue patch (C2) | raised or recessed ring-and-dot pattern marking where glue goes, to cut assembly errors | `[video]` |
| Relief bead (C3) | groove 0.5–1.0 wide × 0.5 deep around the bond area to trap excess (hot glue) | `[video; size judgment]` |
| Injection channel (C3) | internal channel from an outside port to the bond line, vent at the far end; Ø1.5–2 mm thin CA, Ø2.5–4 mm epoxy or hot glue; teardrop section if horizontal; can route into a threaded-insert hole for thread-lock | `[video; sizes judgment]` |

## Adhesive notes `[source: Henkel Design Guide for Bonding Plastics]`
Thicker bond lines lower peak stress (stress factor 18.4 at 0.025 mm → 5.9 at 0.25 mm). CA cures fastest thin (≤ 0.1 mm) and may stress-crack some plastics; use gel or two-part CA for gaps. Epoxy wants 0.1–0.25 mm on rough FDM faces. Pockets give CA a mechanical key it otherwise lacks.

## Model it
1. Sketch a 0.9–1.2 mm square on the glue pad.
2. Extrude-cut −0.5 mm with a −10 to −20° taper (widening inward).
3. Rectangular-pattern at 2–3 mm pitch across the pad.
4. For channels: sketch a Ø2–3 mm path from an outside face to the bond face, cut, add a Ø1.5 mm vent at the far end.

## Failure modes
- Pockets print closed: opening under 0.9 mm or taper over 45°.
- Glue starves the joint: no relief, parts squeezed metal-to-metal; add a bead.
