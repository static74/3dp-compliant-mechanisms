# Fundamentals: rules every mechanism in this skill obeys

Read this once per design session. Each mechanism file assumes it.

## 1. Provenance tags
`[video]` stated in a Slant 3D video. `[measured]` read from video frames against a known dimension (±range given). `[source: URL]` published guide or datasheet. `[judgment]` engineering judgment, untested on a printer. Keep the tag when you quote a number to the user.

## 2. The design thesis (Slant 3D) `[video]`
Do not tune clearances. Fit changes with filament colour, material, machine, nozzle, infill and layer height. Make geometry that self-centres, wedges or flexes so the part works on any printer. If you are tweaking slicer settings to make a joint fit, the joint is designed wrong.

## 3. Orientation rule for every flexing member
Sketch the flexure profile in the XY plane and extrude it in Z, so bending strain runs along deposited lines and never across layer interfaces. A cantilever built up in Z snaps along layer lines `[video]`. Z-direction break strain is roughly a third to a half of in-plane strain for PLA, ASA and nylon `[source: Polymaker TDS, see docs/research/joint-parameters.md §0.6]`.

## 4. Allowable bending strain (printed, in-plane)
The single-snap and repeated columns are `[derived]`: Bayer's moulded-plastic rules (70 % of yield strain, ×0.6 for repeated use) applied to Prusament/Polymaker XY yield strains. The sustained column is `[judgment]`: no published creep data for printed flexures exists; it is a ceiling chosen so PLA retains force for weeks at room temperature. Nothing here is qualified for creep or fatigue: for a feature that stays loaded, leave one sample closed for 7 days at the service temperature and accept ≤ 20 % force loss, and cycle a releasable snap 100 times before trusting it.
| Material | One-time snap (permanent) | Repeated snap (releasable) | Sustained preload (fins, leaf springs) | Across layers |
|---|---|---|---|---|
| PLA | 2.0 % | 1.2 % | ≤ 0.5 % (creeps) | ≤ 0.5 % |
| PETG | 3.6 % | 2.1 % | ≤ 1.0 % | ≤ 1.0 % |
| ABS (assumed = ASA, no printed yield data) / ASA | 2.0 % | 1.2 % | ≤ 1.0 % | ≤ 0.3–1.0 % |
| Nylon (PA6/CoPA) | 3–4 % `[judgment]` | 2 % `[judgment]` | ≤ 1.0 % | ≤ 0.4 % |
| TPU 95A | ≥ 10 % `[judgment]`; stiffness and retention govern, but still check strain | ≥ 10 % | not characterised | good |
Halve these for a Bayer-style safety factor of 2 on anything a customer will cycle daily. PLA creeps: a PLA flexure left bent for a day does not return. Prefer PETG, ASA or nylon for any feature that stays preloaded.

## 5. Cantilever formulas `[source: Bayer "Snap-Fit Joints for Plastics"]`
Constant-thickness beam: deflection y = 0.67·ε·L²/t. Beam tapered to half thickness at the tip (preferred, 63 % more travel): y = 1.09·ε·L²/t with t the root thickness. Solve for L: L = √(y·t / (k·ε)). Deflection force P = b·t²·E·ε/(6L). Insertion force W = P·(μ + tan α)/(1 − μ·tan α), μ ≈ 0.5 for PLA on PLA `[judgment]`. Return face at or above 63° is self-locking; 90° is permanent. Below L/t ≈ 10 the formula overestimates root strain (it ignores wall compliance), so it is conservative; keep L/t ≥ 5 as a practical floor, and ≥ 25 for springs that must live long. The 1.09 factor is for a taper to exactly half thickness; for any other taper ratio use 0.67 (conservative). Strain form used throughout this skill: ε = 1.5·y·t/L² for a constant-section beam, with L measured from the root to the point where the load is applied, not to the beam tip.

## 6. Thickness quantisation (0.4 mm nozzle) `[source: Prusa KB; PrusaSlicer defaults]`
Model walls in whole perimeter multiples: 0.45, 0.9, 1.35, 1.8 mm (Prusa calls these approximate; two perimeters at 0.2 mm layers measure about 0.86 mm). With PrusaSlicer's default Arachne settings, anything 0.1–0.34 mm is widened to 0.34 mm and features under 0.1 mm vanish; other slicers and edited profiles differ, so inspect the sliced toolpath of every thin feature once before printing a batch. Tip of any tapered beam ≥ 0.9 mm (2 perimeters).

## 7. Clearances (per side, 0.4 mm nozzle, 0.2 mm layers)
| Fit | PLA / PETG | ABS / ASA / nylon | Tag |
|---|---|---|---|
| Snug locating | 0.15–0.20 | 0.25 | `[source: UF Marston Makerspace, Prusa MK4]` |
| Sliding | 0.20–0.25 | 0.30 | same |
| Loose | 0.30–0.40 | 0.40 | same |
| Print-in-place XY (moving parts) | 0.30–0.40 | 0.40–0.50 | `[source: Prusa KB ≥0.3]` |
| Relief gap under a flexure (Z) | 0.3 mm (max 0.5); slicers cut each layer at mid-height, so a gap under one layer height can vanish | same | `[video XKrDUnZCmQQ; source: PrusaSlicer slice_z]` |
| Print-in-place Z (moving parts) | ≥ 2 layers (0.4); 0.5–0.6 under an unsupported roof | same | `[judgment]` |
| Vertical pin in hole (video) | 0.25 mm diametral (0.125/side), up to 0.5 diametral for high-shrink | | `[video]` |
Z gaps quantise to the layer height and the slicer samples mid-layer; snap cavity tops to layer boundaries. Add +0.2 mm to any XY gap within the first two layers, or start the gap above layer 2. A rigid round press fit cannot work on FDM: the allowable interference (ε·d ≈ 0.06–0.12 mm on a 6 mm PLA pin) is below the ±0.2 mm printer accuracy, which is why every joint here flexes `[source: Bayer annular limit + Prusa accuracy]`.

## 8. First layer
Chamfer every edge that touches the bed at 45°, 0.4–0.6 mm `[video; size judgment]`, except footprints narrower than 3 mm (prong flats, fin bottoms, thin arms): leave those square and keep ≥ 0.8 mm of flat contact after all edge treatments, or the first layer has nothing to hold `[judgment]`. Set elephant-foot compensation ≈ 0.2 mm `[source: Prusa KB]`. Keep the bed footprint a simple filleted square: thin T-bars or fins on the bed warp in ABS/ASA `[video]`. Round all vertical corners (R ≥ 2 mm; the Slant lid uses R5) `[measured]`.

## 9. Overhangs
45° chamfer beats a fillet on any downward face because it is a constant overhang `[video]`. Horizontal holes get a teardrop with 45° flats, or a truncated teardrop with a flat ≤ 3 mm `[video + source: Hubs]`. Any flexing flange that projects sideways gets its underside angled ≤ 45° so it needs no support `[video]`.

## 10. Micro-slots: forcing wall-dense regions without slicer settings `[video + source: PrusaSlicer source]`
A modelled 0.2 mm slot survives slicing (PrusaSlicer closes only cracks under 0.098 mm) and receives a perimeter on each face, so the region prints as stacked walls instead of sparse infill. The slot itself stays a modelled void; whether the facing walls fuse is Slant's empirical claim, not a slicer guarantee, and an unfused void that runs into the root is a potential crack path. Treat it as an unqualified reinforcement: use 0.2 mm slots about 1 mm apart from the pin tip through its base and 2–5 mm into the body, and compare one slotted pin against a solid-infill control before relying on it. Never go below 0.1 mm (closed, does nothing) or above 0.2 mm (untested).

## 11. Polyholes for vertical holes `[source: nophead]`
Z-axis holes print undersize from corner cutting. Either add 0.1–0.2 mm, or model the hole as a polygon with n = max(round(2·d), 3) sides and circumradius (d/2)/cos(180°/n).

## 12. Report format
When you deliver a mechanism, give: the chosen mechanism and why; a parameter table with tags; print orientation; CAD steps; a tuning note. Flag every `[judgment]` value as needing one test print.
