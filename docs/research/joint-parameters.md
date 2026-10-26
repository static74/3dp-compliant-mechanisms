# Design numbers for the Slant 3D joint catalog (FDM, 0.4 mm nozzle, 0.2 mm layers)

Purpose: fill the GAPS section of `video2-report.md` ("Ultimate Guide to Connecting 3D Printed Parts", Slant 3D, https://www.youtube.com/watch?v=vsHpiHhB3RU) with cited numbers, so a skill can rebuild each joint without the video.

Research date: 2026-10-26.

## How to read this file

**Source-quality tags.** Every row carries one tag.

- **Primary**: a manufacturer design manual, a filament datasheet, slicer source code, or the slicer's own knowledge base, fetched and read directly.
- **Vendor**: a printing-service or printer-vendor blog, fetched and read directly.
- **Video**: stated in the Slant 3D video itself (taken from video2-report.md).
- **Search-summary**: a number that appeared only in a web-search summary. I did not fetch or read the page. Verify it before you rely on it.
- **DERIVED**: computed from cited inputs with a formula shown in this file.
- **UNSOURCED — engineering judgment**: no source found. The value is my recommendation.

**Clearance convention.** This mismatch is the most likely cause of 2x errors, so the convention is fixed for the whole file.

- **Gap (per side)** is the radial or one-wall space between two mating surfaces. The term "gap" in this file always means per side.
- **Diametral clearance** is hole diameter minus pin diameter, which equals 2 x the per-side gap. This file says "diametral" explicitly every time it uses it.
- Each row records how its source stated the value. Many sources do not say, and those rows are marked "convention unstated".

**PrusaSlicer source citations.** Defaults are cited from the legacy option definitions (`src/slic3r-shared/src/Slic3r/Biz/Config/Legacy/PrintConfig.cpp`) at commit 30ef591. The newer `ConfigDefsFDM.cpp` on master confirms min_feature_size 25% and min_bead_width 85%. I did not find `slice_closing_radius` or `elefant_foot_compensation` in that newer file, so confirm those two defaults against your installed version.

**Process assumptions.** The defaults assume a 0.4 mm nozzle, 0.2 mm layers, PrusaSlicer or a similar slicer with the Arachne perimeter generator, and default extrusion widths of about 0.45 mm. Prusa's printer accuracy claim is "at least 0.2 mm" (https://help.prusa3d.com/article/modeling-with-3d-printing-in-mind_164135). Any interference smaller than about 0.2 mm is therefore inside the noise band of the process.

---

## 0. Core formulas (used by every flexing joint below)

### 0.1 Cantilever deflection for a constant-section rectangular beam

The task gives the formula y = ε·L²/(1.5·t). It is correct for a beam of constant thickness, and it derives in two lines:

- Tip deflection is y = P·L³/(3·E·I), with I = b·t³/12. Substituting gives y = 4·P·L³/(E·b·t³).
- Root strain is ε = M·c/(E·I) = 6·P·L/(E·b·t²). Solving for P and substituting gives **y = (4/6)·ε·L²/t = 0.67·ε·L²/t**.

Bayer's "Snap-Fit Joints for Plastics" Table 1 uses the same relation, and Synectic quotes it as Y = 0.67·ε·L²/H.

### 0.2 Cantilever deflection for a beam tapered to half thickness at the tip (the recommended shape)

The tapered beam uses **y = 1.09·ε·L²/t**, where t is the root thickness. Do **not** combine the 0.67 formula with a tapered beam.

Consistency check: 1.09/0.67 = 1.63. Bayer states that the half-thickness taper "increases the permissible deflection by more than 60% compared to a snap-fitting arm of constant cross section." The ratio and the claim agree.

### 0.3 Deflection force and mating force (Bayer)

- Deflection force (rectangular section, used by Bayer for the tapered hook as well): **P = b·t²·E_s·ε / (6·L)**. E_s is the secant modulus at the design strain. A datasheet tensile modulus overestimates E_s, and therefore overestimates P.
- Mating (insertion) force: **W = P·(μ + tan α)/(1 − μ·tan α)**. α is the lead (insertion) angle. Separation force uses the same equation with the return angle α′.
- Self-locking condition: when μ·tan α′ ≥ 1, the joint cannot be pulled apart by axial force. For μ = 0.5, that threshold is α′ = arctan(1/0.5) = **63.4°** (DERIVED). A 90° return face is always permanent.

### 0.4 Permissible strain rules (Bayer)

- A single, brief snap operation may strain amorphous polymers to about **70% of the yield strain**. Partially crystalline polymers may go almost to the yield point. Glass-filled polymers may go to about half the elongation at break.
- For **frequent separation and rejoining, use about 60%** of the single-snap values.
- Bayer's worked example designs for **one-half** of the permissible strain, which is an extra safety factor of 2.
- After assembly the snap feature "should return to a stress-free condition". Grip fins, spring T-slots and crush ribs break that rule because they stay preloaded (see the sustained-strain row in section 3).

### 0.5 Annular (rigid press-fit) limit (Bayer)

Bayer gives the permissible undercut of an annular snap as **y_pm = ε_pm·d**, assuming one part stays rigid. When both parts have equal stiffness, each takes half of the deflection, so the undercut can be twice as large.

Sources for section 0:

| Item | Value | Source | Tag |
|---|---|---|---|
| Constant-beam formula | y = 0.67·ε·L²/t | Bayer "Snap-Fit Joints for Plastics – A Design Guide", Table 1 (MIT-hosted copy): https://fab.cba.mit.edu/classes/S62.12/people/vernelle.noel/Plastic_Snap_fit_design.pdf ; also Synectic https://synectic.net/?p=42601 | Primary (Bayer); Search-summary (Synectic) |
| Tapered-beam formula, h to h/2 | y = 1.09·ε·L²/h, worked example: L 19 mm, y 2.4 mm, ε 2% gives h = 3.28 mm | Bayer guide p.16, Calculation example I (URL above) | Primary |
| Taper benefit | ">60%" more deflection than constant section | Bayer guide p.12 | Primary |
| Taper alternative | width taper to 1/4 of the root width | Bayer guide p.8 | Primary |
| Amorphous strain rule | about 70% of yield strain (single snap); semicrystalline almost to yield | Bayer guide p.11 | Primary |
| Repeated-use factor | 0.6 x single-snap value | Bayer guide Table 2 note, p.12 | Primary |
| Reference strains (molded) | PC 4%, PC/ABS 2.5%, PC blends 3.5%, high-heat PC 4%, PC+10% GF 2.2%, PC+20% GF 2.0% | Bayer guide Table 2, p.12 | Primary |
| Mating force | W = P·(μ+tanα)/(1−μ·tanα) | Bayer guide p.14 | Primary |
| Friction (plastic on steel) | ABS 0.50–0.65 (x1.2 same-on-same), PC 0.45–0.55 (x1.2), PA 0.30–0.40 (x1.5), POM 0.20–0.35 | Bayer guide Table 3, p.15 | Primary |
| Classical formula validity | accurate when L/t > 10:1; overestimates root strain on stubby beams because it ignores wall deformation | BASF via UL Prospector: https://ulprospector.ul.com/1248/snapfit-3/ | Primary (BASF-paid article) |
| Z-built cantilever derate | reduce allowable strain by 50% (elongation at break drops about 50% in Z) | Fictiv via Core77: https://www.core77.com/posts/65318/how-to-design-snap-fit-components | Vendor |

---

## 0.6 Printed-material strain inputs (datasheet values)

The orientation trap matters here. Prusament's "Vertical xz" specimen is printed on edge, so its layers still run along the specimen length and it is **not** an interlayer test. Interlayer (Z) values come only from the Polymaker and Azurefilm sheets.

| Material | In-plane (XY) data | Interlayer (Z) data | Source | Tag |
|---|---|---|---|---|
| PLA (Prusament) | Yield strain 2.9 ± 0.3% horizontal (3.2% xz on edge); yield 51 MPa; E 2.3 GPa | not tested | Prusament PLA TDS v1.1: https://www.matterhackers.com/r/xFvGl8 | Primary |
| PLA (PolyLite) | E 3427 MPa; break 6.3% | break **1.8%**; E 3065 MPa; strength 40.5 MPa | https://wiki.polymaker.com/polymaker-products/more-about-our-products/documents/technical-data-sheets/pla/polylite-tm-pla.md | Primary |
| PETG (Prusament) | Yield strain **5.1 ± 0.1%**; yield 47 MPa; E 1.5 GPa | not tested | Prusament PETG TDS v1.1 (reseller copy): https://www.3dprintergear.com.au/assets/files/technical-data-sheet%20(1).pdf | Primary |
| PETG (PolyLite) | E 2117 MPa; break 8.4% | break **3.3%**; E 1899 MPa | https://wiki.polymaker.com/polymaker-products/more-about-our-products/documents/technical-data-sheets/petg-pet/polylite-tm-petg | Primary |
| ABS (PolyLite) | E 2247 MPa; strength 33.4 MPa; break 17.9%; no yield strain listed | break **3.1%** | https://wiki.polymaker.com/polymaker-products/more-about-our-products/documents/technical-data-sheets/abs-asa/polylite-tm-abs.md | Primary |
| ASA (PolyLite) | E 2379 MPa; break 6.7% | break **1.65%** | https://wiki.polymaker.com/polymaker-products/more-about-our-products/documents/technical-data-sheets/abs-asa/polylite-tm-asa.md | Primary |
| ASA (Azurefilm ASA Prime) | strain at yield **2.9%** XY, 3.2% XZ; E 1900 MPa | strain at yield **0.6%** ZX; strength 9.4 MPa | https://azurefilm.com/wp-content/uploads/2024/04/TDS-ASA-Prime.pptx.pdf | Primary |
| Nylon CoPA (PolyMide) | E 2703 MPa dry; break 12.7% | break **1.3%** | https://wiki.polymaker.com/polymaker-products/more-about-our-products/documents/technical-data-sheets/nylon/polymide-tm-copa.md | Primary |
| TPU 95A (PolyFlex) | E 33.6 MPa; break 551% | not listed | https://wiki.polymaker.com/polymaker-products/more-about-our-products/documents/technical-data-sheets/tpu/polyflex-tm-tpu95.md | Primary |

### Derived design strains (in-plane bending, layers along the beam)

The derivation chain is: ε_single = Bayer amorphous rule (0.7 x XY yield strain). Then ε_repeat = 0.6 x ε_single. Treating printed PLA as amorphous is a judgment call, because printed PLA is mostly amorphous but can partly crystallize. The Z column caps strain at about 1/3 of the Z elongation at break, because Z failure is brittle delamination with no yield.

| Material | ε_single (one-time permanent snap) | ε_repeat (releasable, many cycles) | If bending strain crosses layers (Z); this column is DERIVED with an unsourced judgment factor of 1/3 x Z break | Tag |
|---|---|---|---|---|
| PLA | **2.0%** (0.7 x 2.9) | **1.2%** | ≤ 0.5% (PolyLite Z break 1.8%). Avoid this orientation. | DERIVED |
| PETG | **3.6%** (0.7 x 5.1) | **2.1%** | ≤ 1.0% (Z break 3.3%) | DERIVED |
| ABS | **≈2.0%** (no printed yield strain was found; assumed similar to ASA) | **≈1.2%** | ≤ 1.0% (Z break 3.1%) | DERIVED from ASA plus UNSOURCED assumption |
| ASA | **2.0%** (0.7 x 2.9) | **1.2%** | ≤ 0.3% (ZX yield strain 0.6%). Avoid this orientation. | DERIVED |
| Nylon (CoPA, PA6/66) | **≈3–4%** (semicrystalline, so close to yield; yield strain not published) | **≈2%** | ≤ 0.4% (Z break 1.3%) | UNSOURCED — engineering judgment (bounded by the 12.7% XY break) |
| TPU 95A | ≥ 10%. Strain rarely governs; design for stiffness and retention instead. | ≥ 10% | layer adhesion is good, but still keep it in-plane | UNSOURCED — engineering judgment |

For the Bayer-style conservative design, halve these values (the Bayer worked example uses ε = ½·ε_pm). Halving PLA gives about 1% repeated, which matches the task's "PLA about 1–2%".

**Orientation rule (applies to every flexing feature).** Sketch the beam profile in the XY plane and extrude it in Z, so that bending strain runs along the deposited lines and never across layer interfaces. Hubs says to avoid cantilevers built vertically in Z (https://www.hubs.com/knowledge-base/how-design-snap-fit-joints-3d-printing). Kuumeri prints flexures standing vertical and recommends "If you must print flexures laying flat, make sure the print lines are longitudinal" (https://s3files.core77.com/images/c77_webinar_series/Akaki-Kuumeri-3D-printed-flexures.pdf). The video's report infers the same rule for the forked pin (D5).

---

## 1. Cantilever snap-fit

Joints covered: C-clamp clip (A4), S-bracket hooks (A3), "Snap In" bi-directional locking tab (B6), forked detent pin (D5).

| Parameter | Recommended value | Material notes | Source URL | Tag |
|---|---|---|---|---|
| Deflection formula, constant section | y = 0.67·ε·L²/t | all materials | Bayer guide (section 0) | Primary |
| Deflection formula, tapered to t/2 | y = 1.09·ε·L²/t (root t) | all materials | Bayer guide p.16 | Primary |
| Taper | Linear taper in thickness to **0.5 x root** at the hook, or a width taper to 0.25 x root | On FDM, keep the tip ≥ 2 perimeters (0.9 mm), so the root should be ≥ 1.8 mm | Bayer guide p.8; perimeter widths from https://help.prusa3d.com/article/modeling-with-3d-printing-in-mind_164135 | Primary + DERIVED |
| Root thickness, minimum | **≥ 1 mm** (Hubs, written for MJF). FDM: use whole-perimeter multiples, 0.9 / 1.35 / 1.8 mm | PLA, ASA: thinner and longer is better because the allowed strain is low | Hubs: https://www.hubs.com/knowledge-base/how-design-snap-fit-joints-3d-printing ; Prusa KB perimeters 0.45 / 0.9 / 1.35 / 1.8 mm | Vendor + Primary |
| Width, minimum | **≥ 5 mm** | narrower beams twist; Kuumeri uses ≥ 10 mm for flexures | Hubs (above); Kuumeri PDF | Vendor |
| L/t ratio | **≥ 10:1** keeps the formula accurate. Typical ranges are 8–10:1 for PLA and 5–8:1 for PETG (Sovol). DERIVED check: PLA, t = 1.5 mm, y = 1.0 mm, ε_repeat 1.2% gives L = 13.7 mm, so L/t ≈ 9. | lower strain means a longer beam | BASF via UL Prospector https://ulprospector.ul.com/1248/snapfit-3/ ; Sovol https://www.sovol3d.com/blogs/news/3d-printed-snap-fit-joints-how-to-design-clips-that-work | Primary + Search-summary + DERIVED |
| Allowable strain | see the derived table in section 0.6: PLA 2.0 / 1.2%, PETG 3.6 / 2.1%, ABS-ASA 2.0 / 1.2%, nylon about 3–4 / 2% | halve the value for a Bayer-style safety factor of 2; Z-built beams ≤ 0.3–1% | section 0.6 | DERIVED |
| Root fillet | **R ≥ 0.5 x root thickness** (Hubs). Stress-concentration benefit plateaus at **R/t ≈ 0.6** (Bayer). Absolute minimum **0.38 mm** (0.015 in, Bayer) | FDM has no sink-mark penalty, so use R/t = 0.6 freely | Hubs (above); Bayer guide p.8 | Vendor + Primary |
| Hook undercut depth (= y) | **0.8–1.2 mm**. The undercut must exceed the mating gap plus the ±0.2 mm print accuracy. Hubs (MJF) gives ≥ 1 mm overhang. | Do not go below 0.6 mm on FDM, or the catch becomes unreliable | Hubs (above); Prusa KB accuracy 0.2 mm | Vendor + DERIVED |
| Insertion (lead) angle α | **30°** (Bayer worked example uses α = 30°; Bayer's annular example treats a rounded 45° edge as about 30° effective). Allowed range 20–35°. | lower α gives lower insertion force | Bayer guide p.16, p.21 | Primary |
| Return angle α′, permanent | **90°** (BASF: "a 90° return angle to avoid bending"). Any α′ ≥ 63° is self-locking at μ = 0.5. | Use with an external release window if service is needed | BASF via UL Prospector; Fictiv via Core77; DERIVED self-locking | Primary + DERIVED |
| Return angle α′, releasable | **35–45°**. α′ = α gives equal insert and remove force (Fictiv). With μ = 0.5, α′ = 45° gives W ≈ 3·P; α′ = 60° gives W ≈ 16·P, which is effectively permanent. | "Bi-directional" tab B6 needs α′ ≈ 40–45° | Core77/Fictiv (above); DERIVED from Bayer W formula | Vendor + DERIVED |
| Mating clearance (gap) | **0.3 mm** for a close-fit snap (Fictiv); **0.5 mm** nominal for FDM (Hubs, convention unstated); 0.25 mm PLA/PETG open-frame, 0.35 mm ABS in a heated chamber (Qidi) | ABS, ASA, nylon need more because they shrink more (Qidi suggests 0.3–0.5 mm) | Core77/Fictiv; Hubs; Qidi https://qidi3d.com/blogs/print-lab/3d-printed-snap-fit-joints-clearance-guide | Vendor (Fictiv, Hubs); Search-summary (Qidi) |
| Friction μ (same-on-same) | PLA: **0.5**. ABS 0.6–0.78 (0.50–0.65 x 1.2), PA 0.45–0.6 | PLA is not in the Bayer table | Bayer Table 3; PLA value UNSOURCED | Primary + UNSOURCED |
| Print orientation | profile in XY, extruded in Z; the hook flank or underside at ≤ 45° from vertical, so no supports are needed (video B6: "angled them on the bottom") | — | Video; Hubs 45° overhang https://www.hubs.com/knowledge-base/how-design-parts-fdm-3d-printing/ | Video + Vendor |

### 1.1 Worked example (copy this calculation for any tab)

The example is a PLA releasable locking tab, printed flat with the profile in XY. It tapers from t = 1.8 mm (4 perimeters) at the root to 0.9 mm at the hook, with width b = 6 mm and undercut y = 0.8 mm.

1. Design strain: ε_repeat = 1.2%.
2. Tapered-beam length: L = √(y·t/(1.09·ε)) = √(0.8 x 1.8 / (1.09 x 0.012)) = √110 = **10.5 mm**. A constant-thickness beam would need √(1.44/(0.67 x 0.012)) = **13.4 mm**.
3. Deflection force: P = b·t²·E·ε/(6L) = 6 x 1.8² x 2300 x 0.012 / (6 x 10.5) ≈ **8.5 N**. This is an upper bound because the secant modulus is below 2.3 GPa.
4. Insertion force at α = 30° and μ = 0.5: W = 8.5 x (0.5 + 0.577)/(1 − 0.289) ≈ **13 N**.
5. Removal force at α′ = 45°: W = 8.5 x 1.5/0.5 ≈ **26 N**. At α′ = 90° the tab is permanent.
6. Root fillet: R = 0.6 x 1.8 ≈ **1.1 mm**.

### 1.2 Joint-specific notes

- **C-clamp (A4).** Each tine is a cantilever with the formulas above. Both tines flex, so each takes half of the total closing deflection (Bayer's equal-stiffness rule). DERIVED.
- **S-bracket (A3).** The S-bracket is a curved or U-shaped spring. Bayer's U-shaped arm (Fig. 15) and BASF's U/L-shaped designs (BASF manual pp. V-1 to V-4, not obtained) apply. A practical approximation treats each leg as a cantilever measured from the bend. The video's "compression" means the free length is shorter than the pocket spacing. Use about 0.3–0.5 mm of interference, so the bracket still contacts after a ±0.2 mm print error. UNSOURCED — engineering judgment.
- **Forked detent pin (D5).** Each prong is a cantilever. The detent bump height equals y. Use **0.3–0.5 mm** for a "pop" detent, with α = α′ ≈ 30–45° so it releases. Each prong needs ≥ 2 perimeters (0.9 mm), and the slot between prongs must be ≥ 2y so both prongs can close fully. Bump height is UNSOURCED — engineering judgment; the prong mechanics are DERIVED.
- **Locking tab "Snap In" (B6).** The tab sits on the bed with its flanges projecting sideways. The flange undersides are chamfered at ≤ 45° from vertical, so they need no support. The video states this in words only; the angle is from Hubs and Prusa.

---

## 2. Press-fit pins and holes

Joints covered: diamond peg (A1), slab (A2), horizontal pins (D1–D4), vertical pins (E2), cruciform pin (E3), fluted pin (E4).

| Parameter | Recommended value | Material notes | Source URL | Tag |
|---|---|---|---|---|
| Vertical-pin hole clearance | **0.25 mm** default, **up to 0.5 mm** for high-shrink material. The plain reading is diametral (hole "a hair larger" than the pin), which is **about 0.125 mm per side**. | 0.5 mm suits ABS, ASA, nylon | Video E2 (26:00) | Video |
| Standard sliding fit (separate parts) | **0.20–0.25 mm** for tabs, rails, enclosures | Prusa MK4/XL tested | UF Marston Makerspace: https://makerspace.uflib.ufl.edu/services/3dprocess/recommended-software-for-3d-printing/designing-for-3d-printing-tolerances-on-the-mk4-and-xl/ (convention unstated; reads as per-side gap) | Primary (university lab) |
| Snug / locating fit | **0.15–0.20 mm** ("very dependent on surface qualities") | — | UF (above) | Primary (university lab) |
| Loose fit | **0.30–0.40 mm** for covers and adjustable parts | — | UF (above) | Primary (university lab) |
| Onshape-forum fit guidance | about 0.2 mm rigid, about 0.5 mm sliding | — | https://forum.onshape.com/discussion/comment/79373 | Search-summary |
| Rigid interference fit limit | Bayer y_pm = ε·d. For a 6 mm PLA pin, ε = 1–2% gives **0.06–0.12 mm**, which is below the ±0.2 mm print accuracy. A rigid round press fit cannot be held reliably on FDM. This is the quantitative argument for the video's compliant features (crush ribs, forks, cross pins that wear in). | — | Bayer guide p.20; Prusa KB accuracy | DERIVED |
| Snapmaker interference guidance | 0.0 to −0.05 mm (intentional overlap) for press fits | consistent with the DERIVED limit above | https://www.snapmaker.com/blog/3d-printing-tolerances | Search-summary |
| Vertical-axis hole (axis in Z) shrinkage | prints **undersized**. The dominant cause is the nozzle cutting corners on a circular path; polygon faceting shrinks the radius by cos(π/n). | all materials | nophead "Polyholes": https://hydraraptor.blogspot.com/2011/02/polyholes.html ; Hubs FDM guide (print undersized, drill critical holes) https://www.hubs.com/knowledge-base/how-design-parts-fdm-3d-printing/ | Primary (originator) + Vendor |
| Polyhole correction | **n = max(round(2·d), 3) sides, r_poly = (d/2)/cos(180°/n)** (d in mm). "You need 10 vertices to reduce the [faceting] error to 5% and 22 for 1%." | — | nophead (above) | Primary |
| Measured undersize, small vertical holes | about **0.1 mm** with Arachne, **0.3–0.4 mm** with the Classic generator (2–4 mm PLA holes) | — | MakerWorld forum post: https://makerworld.com/en/community/post/1249520 | Search-summary (forum) |
| Horizontal-axis hole (axis in XY) | The top of the hole sags. Use a **teardrop** with **45° flats** (90° included apex), or truncate the apex with a flat bridge. Hexagon with flat top and bottom: 60° max overhang. | Prusa Nextruder printers manage overhangs up to 75°, but use 45° for any printer | Prusa forum via search: https://forum.prusa3d.com/forum/original-prusa-i3-mmu2s-mmu2-how-do-i-print-this-printing-help/print-fails-at-height ; Fabbaloo (Zaggo truncated teardrop) https://www.fabbaloo.com/blog/2011/12/14/the-new-teardrop-html ; video D1 shows a teardrop ("small corner up on top, fairly shallow") | Search-summary + Video |
| Truncated teardrop flat | Choose a flat width ≤ a few mm. Hubs warns of sagging above **5 mm** bridges. | — | Hubs FDM guide (above) | Vendor |
| Teardrop sag allowance | Offset the hole outward by about 1 layer height (0.2 mm), or about 2 layers at fine layer heights | — | Bambu forum: https://forum.bambulab.com/t/holes-are-not-printed-cleanly/190851 | Search-summary |
| Pin tip lead-in | **45° chamfer**, which is a "consistent overhang of 45°" rather than a fillet. Size 0.5–1.0 mm, or about 10–15% of the pin diameter. | — | Video D1 (18:28) for the angle; size UNSOURCED — engineering judgment | Video + UNSOURCED |
| Hole lead-in | 45° chamfer or fillet funnel, 0.5–1.0 mm | — | Video E2 (funnel); Prusa KB ("chamfering the edges of parts that slot together eases assembly"); size UNSOURCED | Video + Primary + UNSOURCED |
| Pin draft (vertical pins) | **1.5°** (Shapr3D panel value on the cross pin). The range is **1–2°**. The base is wider than the hole and the tip narrower, so the pin wedges. | — | Video E3 (29:12 panel); Siraya https://siraya.tech/blogs/news/3d-print-joints | Video + Search-summary |
| Pin base fillet | **R ≈ 0.5–0.6 x pin wall** (Bayer R/h 0.6 plateau, Hubs ≥ 0.5t). Practical **0.5–1.0 mm**. Hubs: add a fillet to any pin under 5 mm. | the hole needs a matching chamfer or countersink | Bayer p.8; Hubs FDM guide; video E2 | Primary + Vendor + Video |
| Minimum pin diameter | **≥ 5 mm** if the pin must have perimeters plus infill. Below 5 mm, fillet the base and print it solid (or use the 0.2 mm micro-slot trick, section 7). | — | Hubs FDM guide (above) | Vendor |
| Pin length (vertical pins) | as short as possible; **L/d ≤ 1–1.5** | vertical pins fail in interlayer shear at the base | Video E2 (27:25); ratio UNSOURCED — engineering judgment | Video + UNSOURCED |
| Horizontal pin orientation | print the pin lying flat (its axis in XY), so layers run along the pin. Square or diamond pins rotated 45° need no support. | — | Video A1, D | Video |
| Cross-pin arm width | **≥ 2 perimeters (0.9 mm)**, typically **1.35–2.0 mm** (3–4 perimeters), so each arm prints as solid walls | — | Prusa KB perimeter widths; the video's slicer view shows 2–3 perimeters per arm | Primary + Video (ESTIMATED) |
| Elephant-foot effect on bed-side holes and pins | apply about 0.2 mm EFC, **and** chamfer the bed edge 45° x (≥ 0.4 mm) | — | section 8 | Primary |

---

## 3. Grip fins and crush ribs inside a pocket

Joint covered: eye slot with grip fins (B5). Crush ribs are included because they are the same tolerance-absorbing idea.

| Parameter | Recommended value | Material notes | Source URL | Tag |
|---|---|---|---|---|
| Fin thickness | **0.45 mm (1 perimeter)** for a soft grip, or **0.9 mm (2 perimeters)** for a firm grip. Never model 0.1–0.34 mm: Arachne widens any feature from 0.1 mm up to the 0.34 mm minimum perimeter width (85% of the nozzle), so the fin becomes stiffer than designed. Features below 0.1 mm (25% of the nozzle) are dropped. | single-line walls are fragile in PLA; prefer PETG | Prusa KB perimeter widths https://help.prusa3d.com/article/modeling-with-3d-printing-in-mind_164135 ; PrusaSlicer defaults min_feature_size 25%, min_bead_width 85%: https://github.com/prusa3d/PrusaSlicer/blob/30ef59195e0f3ee6f270b185bb5f9fb5f349f81f/src/slic3r-shared/src/Slic3r/Biz/Config/Legacy/PrintConfig.cpp#L4050 and #L4062 ; Arachne KB https://help.prusa3d.com/article/arachne-perimeter-generator_352769 | Primary |
| Kuumeri flexure primitive (calibration point) | 0.75 mm thick ("exactly two lines wide"), 40 mm long, 5 mm tip displacement, ≥ 10 mm wide, always printed vertically. DERIVED strain = 1.5·y·t/L² = **0.35%**. | PLA+: "PETG is said to be more flexible (yields later, creeps less)" | Kuumeri PDF https://s3files.core77.com/images/c77_webinar_series/Akaki-Kuumeri-3D-printed-flexures.pdf | Primary (practitioner) + DERIVED |
| Fin free length | Solve L = √(y·t/(0.67·ε_sustained)), using the sustained strain from the next row, not ε_single. **PLA (ε = 0.5%):** t = 0.45 gives **6.3 mm** at y = 0.3 and **8.2 mm** at y = 0.5. t = 0.9 gives 9.0 mm and 11.6 mm. **PETG (ε = 1%):** t = 0.45 gives **4.5 mm** and **5.8 mm**. t = 0.9 gives 6.3 mm and 8.2 mm. PLA fins at t = 0.9 are too long to fit radially in a Ø20 mm eye, so use t = 0.45 for PLA, or switch to PETG. | longer fins grip more softly and creep less | DERIVED (formula 0.1) | DERIVED |
| Sustained (preload) strain | **≤ 0.5% PLA, ≤ 1% PETG, ABS, ASA**. Fins stay bent indefinitely, which breaks Bayer's "return to stress-free" rule. Kuumeri: PLA plastics "creep easily… Leave a flexure bent for a day, and it won't return to center… Never leave under tension." | prefer PETG, ABS, ASA, nylon for preloaded features | Kuumeri PDF; Bayer p.3 | UNSOURCED — engineering judgment (motivated by primary sources) |
| Interference per fin (radial) | **0.3–0.5 mm**. It must exceed the ±0.2 mm print accuracy, so every fin still touches when parts print oversize or undersize. | — | Prusa KB accuracy; value UNSOURCED — engineering judgment | UNSOURCED |
| Fin count | about **15** around a Ø20 mm eye. Use **8–16**, spaced **≥ 3 mm** at the tips. | — | Video B5 (ESTIMATED from frames); range UNSOURCED | Video (estimate) + UNSOURCED |
| Fin angle | tangential lean of **30–45° from radial** (iris or fan pattern), so the tongue bends the fins instead of crushing them end-on | — | Video B5 frames (ESTIMATED); value UNSOURCED | UNSOURCED |
| Fin leading-edge chamfer | 45° chamfer on the insertion side (the video uses a two-distance chamfer); make it about half the fin length | — | Video B5 (8:03 panel); size UNSOURCED | Video + UNSOURCED |
| Gap from fin to roof or floor | **≥ 2 layers = 0.4 mm** at 0.2 mm layers (0.6 mm is safer). Z gaps quantize to the layer height: a modeled 0.3 mm gap prints as either 0.2 or 0.4 mm. The fin must be detached from the skin to work as a cantilever (video: fins "cannot be connected to the roof"). | — | Video B5; value UNSOURCED — engineering judgment | Video + UNSOURCED |
| Crush-rib mechanism | Most of the compliance comes from the **surrounding wall bending inward**, not from the rib crushing. Model ribs straight, with no draft. Bayer's equal-stiffness rule applies: rib and wall each take part of the interference. | — | Printables test (via search) https://www.printables.com/prints/43636-test-print-crush-ribs-version04 ; Hackaday on Royer https://hackaday.com/tag/press-fit , original https://www.marginallyclever.com/2020/09/have-you-heard-of-crush-ribs/ | Search-summary + Vendor |
| Crush-rib interference | **0.2–0.3 mm** (radial) to start, then test | — | Lemmy user (via search) https://lemmy.nekusoul.de/post/1629502/4656980 | Search-summary (forum) |
| Crush-rib geometry | 3–6 ribs, rib width 0.9–1.35 mm (2–3 perimeters), semicircular or triangular tip, a 45° lead-in at the mouth, wall behind ribs 1.2–2 mm | — | UNSOURCED — engineering judgment | UNSOURCED |

---

## 4. Leaf-spring / curved-flange flexible T-slot

Joint covered: flexible T-slot (B3), the joint the video calls "springs".

| Parameter | Recommended value | Material notes | Source URL | Tag |
|---|---|---|---|---|
| Flange model | Treat each curved flange as a cantilever measured from the neck, with free length L equal to the arc length. The curvature adds compliance, so the straight-beam formula is conservative. Bayer covers curved arms only through its ring-segment section (Table 1 shape C, worked example II: y = 1.64·K₂·ε·L²/r₂). | — | Bayer guide p.17 | Primary (method) |
| Flange thickness | **0.9–1.35 mm** (2–3 perimeters), tapering toward the tip if possible | PLA: thinner and longer | Prusa KB perimeter widths; value UNSOURCED | Primary + UNSOURCED |
| Flange arc | arc radius about 1–1.5 x the T-bar half-width. A circle of about 1.6–2 x the neck width, trimmed (video sketch at 6:41). | — | Video B3 (ESTIMATED) | Video (estimate) |
| Interference (preload) | **0.3–0.5 mm** at each flange tip. Check flange strain with y = 0.67·ε·L²/t against **ε_sustained** (section 3). Example: PETG, t = 0.9 mm, y = 0.4 mm, ε = 1% gives **L ≥ 7.3 mm**. | permanent preload, so prefer PETG, ABS or ASA; PLA will relax | DERIVED; interference UNSOURCED | DERIVED + UNSOURCED |
| Slot tilt for printability | Tilt the slot so the first layer is a simple filleted square and every overhang stays ≤ 45°. Estimated tilt **20–30°**. | — | Video B3 (stated qualitatively; angle ESTIMATED); 45° rule from Hubs | Video + Vendor |
| Flange chamfers | 45° on the outer flange edges and the lead-in | — | Video B3 ("chamfered as well"); 45° per video D1 | Video |
| Neck clearance (rigid part of the T) | 0.2–0.3 mm per side, so only the springs locate the joint | — | UF sliding fit; Qidi (0.20–0.30 mm per side for sliding parts) | Primary + Search-summary |

---

## 5. Dovetail, tongue-and-slot, T-slot

Joints covered: basic tongue (B1), T-slot (B2), eye slot (B4), slab (A2).

| Parameter | Recommended value | Material notes | Source URL | Tag |
|---|---|---|---|---|
| Sliding clearance | **0.20–0.30 mm per side**. Friction "rises sharply below 0.20 mm". | ABS, ASA, nylon at the top of the range | Qidi https://qidi3d.com/en-br/blogs/news/how-to-3d-print-interlocking-parts-and-assemblies ; UF 0.20–0.25 mm standard sliding | Search-summary + Primary |
| Dovetail flank angle | **15° per side from vertical** (a 75° interior angle), range 10–20°. **Keep the overhanging dovetail face ≤ 45° from vertical** when the slot is printed open-side up. | — | UNSOURCED — engineering judgment (no FDM-specific source found). The 45° overhang limit is from Hubs. | UNSOURCED |
| Lengthwise taper (self-tightening) | **1–2°** along the slide, so the joint starts loose and finishes tight | the same idea as the video's chamfered, wedging tongues | Siraya https://siraya.tech/blogs/news/3d-print-joints | Search-summary |
| Leave one face at zero clearance | Ease the side faces and leave one locating face tight. A loose fit wobbled; a tight fit distorted the angles. | — | Duet3D forum https://forum.duet3d.com/post/12551 | Search-summary (forum) |
| Chamfer / lead-in | 45° x 0.5–1.0 mm on the tongue tip and the slot mouth | — | Video B1/B2 ("chamfer… so it wedges in"); size UNSOURCED | Video + UNSOURCED |
| Internal-corner relief | Add "mouse ears" (dog-bone or circular reliefs) at the slot's internal corners, because FDM cannot print sharp inside corners | — | UF Marston Makerspace (above) | Primary (university lab) |
| First-layer compensation | elephant-foot compensation **≈0.2 mm** (Prusa KB) plus a 45° chamfer on bed-side slot edges | high-warp ABS and ASA: keep a simple first layer (video B2/B3) | section 8 | Primary |
| Eye (round) tongue | One circle dimensions the joint ("one single circle that is dead center"). Ø20 mm eye in a 25 mm block. Clearance about 0.2 mm per side, and the neck 0.2–0.3 mm per side. | — | Video B4 (Ø20.00 and 25.00 STATED); clearances from UF | Video + Primary |

---

## 6. Glue pockets and glue channels

Features covered: dovetail relief pockets (C1), directed glue patches (C2), internal channels (C3).

| Parameter | Recommended value | Material notes | Source URL | Tag |
|---|---|---|---|---|
| Pocket depth | **0.5 mm** (video cut −0.5 mm) to 1.0 mm | — | Video C1 (STATED −0.5 mm) | Video |
| Pocket opening | **≥ 0.9 mm** (2 extrusion widths) so the slicer keeps it open. A 0.45 mm hole is marginal. | — | Prusa KB perimeter widths; DERIVED | DERIVED |
| Undercut taper | Widen the pocket with depth by **10–20°** per wall (extrude-cut with a negative taper). Keep each widening wall **≤ 45° from vertical** so it prints without support. | — | Video C1 (taper used, value not shown); 45° limit from Hubs; value UNSOURCED | UNSOURCED |
| Pocket pitch | **2–3 mm** (land ≥ 0.9 mm between pockets) | about 15 x 15 pockets across a pad in the video | Video C1 (count ESTIMATED); pitch UNSOURCED | UNSOURCED |
| Bond-line thickness effect | A thicker bond line lowers peak shear stress. In Henkel's table for plastic lap joints, stress ratio is 18.4 at 0.001 in, 13.0 at 0.002 in, 8.31 at 0.005 in, 5.93 at 0.010 in, 4.25 at 0.020 in. A 0.010 in (0.25 mm) bond line with a flexible adhesive gave a stress factor of 1.64, comparable to bonded steel. | favors epoxy at 0.1–0.25 mm over CA in thin films on FDM's rough faces | Loctite Design Guide for Bonding Plastics Vol. 5, pp. 80, 88: https://dm.henkel-dam.com/is/content/henkel/Design-Guide-Bonding-Plastics | Primary |
| CA (cyanoacrylate) gap | Thin bond lines cure fastest, and cure slows as the gap grows. Henkel lists "limited gap cure" and "may stress crack some plastics" as CA disadvantages. Keep mating faces ≤ **0.1 mm** apart for thin CA. Use a gel CA or a 2-part CA (Loctite 3092 fills up to **5 mm**) for larger gaps. | — | Henkel guide p.6 (CA advantages/disadvantages table), https://dm.henkel-dam.com/is/content/henkel/Design-Guide-Bonding-Plastics ; Loctite 401 TDS https://www.monet.asia/media/pdf/TDS_LOCTITE-401.pdf ; selector guide https://res.cloudinary.com/iwh/image/upload/q_auto,g_center/assets/1/7/selectionguide.pdf | Primary + Search-summary; the 0.1 mm figure is UNSOURCED |
| Epoxy bond line | **0.05–0.10 mm** gives the highest lap shear (datasheet quote). FDM faces need about 0.1–0.25 mm for full wet-out. | — | Model Engineer forum quoting an unnamed datasheet https://www.model-engineer.co.uk/forums/topic/emgineering-glues/ | Search-summary (forum) |
| Injection channel diameter, thin CA | **Ø1.5–2 mm**, with a vent hole at the far end | horizontal channels need a teardrop profile | UNSOURCED — engineering judgment | UNSOURCED |
| Injection channel diameter, epoxy or hot glue | **Ø2.5–4 mm**. Hot glue needs ≥ 3 mm because it freezes fast. | — | UNSOURCED — engineering judgment | UNSOURCED |
| Glue relief bead (excess trap) | groove 0.5–1.0 mm wide x 0.5 mm deep around the bond area, so the part keeps its stated dimension | — | Video C1/C3 (purpose STATED); size UNSOURCED | Video + UNSOURCED |

---

## 7. Micro-features: the 0.2 mm slot

Feature covered: the fluted pin micro-slot (E4) and the related Slant "microstructure" walls.

| Parameter | Recommended value | Material notes | Source URL | Tag |
|---|---|---|---|---|
| Slot width | **0.2 mm** (video). Secondhand reporting of a related Slant video gives "about 0.2 mm" for the same reason: narrow contour lines merge instead of forming separate walls. | — | Video E4 (30:37); 3printr summary https://www.3printr.com/youtuber-shows-reinforced-wall-structures-for-more-robust-3d-printed-parts-1871735/ | Video + Search-summary |
| Does the slicer close a 0.2 mm slot during slicing? | **No.** PrusaSlicer `slice_closing_radius` defaults to **0.049 mm** and closes only cracks narrower than 2 x 0.049 = **0.098 mm**. A 0.2 mm void survives slicing as a hole. | — | PrusaSlicer source (SHA 30ef591): https://github.com/prusa3d/PrusaSlicer/blob/30ef59195e0f3ee6f270b185bb5f9fb5f349f81f/src/slic3r-shared/src/Slic3r/Biz/Config/Legacy/PrintConfig.cpp#L3288 | Primary |
| What actually happens | (1) The void survives slicing (row above). (2) The slicer places perimeters on both faces of the slot. Each perimeter is about 0.45 mm wide (1.125 x nozzle), and its outer edge sits on the contour, so the nominal printed gap stays 0.2 mm. (3) The region therefore prints as **stacked wall lines instead of sparse infill**, which is the strengthening effect. Whether the two facing walls also physically fuse across the 0.2 mm gap depends on squish and ooze. That fusion is Slant's empirical claim, not something the slicer guarantees. | The trick should work in any slicer that keeps the void | width default: same file, external_perimeter_extrusion_width tooltip ("1.125 x nozzle diameter") #L1113; fusion claim: Video E4 and 3printr summary | Primary + Video + Search-summary |
| What does *not* close it | Arachne `min_feature_size` (default **25% of the nozzle = 0.1 mm**) controls thin **solids**, not voids, so Arachne does not close the slot. "Detect thin walls" (`thin_walls`, default on, disabled under Arachne) also handles solids only. | — | source lines #L4050 (min_feature_size), #L3713 (thin_walls); Arachne KB https://help.prusa3d.com/article/arachne-perimeter-generator_352769 | Primary |
| Gap fill | Gap fill (default on) fills spaces between perimeters and between perimeters and infill. It does not fill a modeled void. | — | source #L1809 | Primary |
| Slots below 0.1 mm | They are closed at slicing and **do nothing**. Never model a strengthening slot under 0.1 mm. | — | DERIVED from slice_closing_radius | DERIVED |
| Wider slots | The wider the slot, the more likely it stays visibly open and acts as a crack starter. **0.2 mm is the value Slant tested.** Do not go wider without testing. | — | Video E4; reasoning UNSOURCED — engineering judgment | Video + UNSOURCED |
| Slot depth | Run the slots from the pin tip down **through the pin base and 2–5 mm into the body** ("deep into this part a little ways"), so the pin root is solid. Stop the slots ≥ 3 top layers (0.6 mm) below any cosmetic top surface. | — | Video E4 (qualitative); values UNSOURCED | Video + UNSOURCED |
| Slot spacing | about 1 perimeter-pair apart (**0.9–1.0 mm**), so the whole region becomes walls | — | UNSOURCED — engineering judgment | UNSOURCED |
| Reported benefit (related Slant test) | circumferential micro-grooves made a cylinder "up to a third more resilient" | — | 3printr summary (above) | Search-summary |

---

## 8. Print-in-place and separable clearances by orientation

| Parameter | Recommended value | Material notes | Source URL | Tag |
|---|---|---|---|---|
| Printer accuracy | "at least 0.2 mm" (Original Prusa) | — | https://help.prusa3d.com/article/modeling-with-3d-printing-in-mind_164135 | Primary |
| Separate parts, snug | 0.15–0.20 mm | — | UF https://makerspace.uflib.ufl.edu/services/3dprocess/recommended-software-for-3d-printing/designing-for-3d-printing-tolerances-on-the-mk4-and-xl/ | Primary (university lab) |
| Separate parts, sliding | 0.20–0.25 mm | — | UF (above) | Primary (university lab) |
| Separate parts, loose | 0.30–0.40 mm | — | UF (above) | Primary (university lab) |
| Separate parts, tight / slide / close snap | 0.2 / 0.4 / 0.3 mm | — | Fictiv via Core77 https://www.core77.com/posts/65318/how-to-design-snap-fit-components | Vendor |
| Print-in-place, XY gap (moving parts, hinges) | **≥ 0.3 mm** (Prusa); "the larger end of standard sliding and loose" (UF). Use **0.3–0.4 mm** for PLA and PETG, **0.4–0.5 mm** for ABS, ASA, nylon. | PETG strings and may need +0.1 mm; TPU needs ≥ 0.5 mm because it sticks to itself (UNSOURCED) | Prusa KB (above); UF (above); material split UNSOURCED | Primary + UNSOURCED |
| Print-in-place, practitioner reports | 0.30–0.40 mm "must never fuse"; below 0.3 mm the layers may weld. Prusa MK4 reliably separates 0.2 mm in PLA; an Ender 3 needs 0.3 mm. | — | https://phorm.to/blog/3d-printing-tolerances-clearances/ ; https://printforgehq.com/print-in-place-3d-printing/ | Search-summary |
| Print-in-place, Z gap (above or below a moving part) | **≥ 2 layers (0.4 mm)** at 0.2 mm layers. Z gaps quantize to the layer height. A downward-facing surface over a gap is a bridge or overhang and sags, so use **0.5–0.6 mm** under unsupported roofs. | — | UNSOURCED — engineering judgment | UNSOURCED |
| Print-in-place, first-layer gap | Add **+0.2 mm** to any XY gap that lies within the first 1–2 layers, or start moving gaps above layer 2. First-layer squish closes gaps on the bed. | — | Prusa EFC KB (squish mechanism); value UNSOURCED | Primary + UNSOURCED |
| Elephant-foot compensation | PrusaSlicer source default is **0**. Official Prusa profiles **enable** it, and Prusa recommends **"around 0.2 mm"** for a 0.4 mm nozzle. Set it to 0.1–0.3 mm. It shrinks only the first layer in XY. | A commenter caps it at about half the first-layer extrusion width. A lower nozzle temperature often helps more for heavy squish. | Prusa KB https://help.prusa3d.com/article/elephant-foot-compensation_114487 ; default in source #L396 (same SHA URL as section 7) | Primary |
| First-layer extrusion width | The source default is **200% of the first-layer height**, which is about 0.4 mm at a 0.2 mm first layer. Printer profiles override this value. Squish on the bed spreads the first layer beyond the commanded width. | the reason bed-side features grow | source #L1690–1702 (`ratio_over = "first_layer_height"`) | Primary |
| Bed-edge chamfer | **45°**, size ≥ 1 first-layer height (0.2–0.3 mm), typically **0.4–0.6 mm**, on every edge touching the bed, so EFC plus the chamfer hides the squish | — | Hubs ("45° chamfer or radius on all edges touching the build plate") https://www.hubs.com/knowledge-base/how-design-parts-fdm-3d-printing/ ; Autodesk (chamfer depends on layer thickness, via search); size UNSOURCED | Vendor + UNSOURCED |
| XY vs Z hole accuracy | Holes with their axis in Z are dimensionally better but undersized from corner cutting. Holes with their axis in XY are rounder only with a teardrop. One small-hole study (0.8 mm PLA) found vertical printing gave better diameter accuracy and horizontal printing better roundness. | — | IEOM 2026 conference paper https://ieomsociety.org/proceedings/ankara2026/55.pdf | Search-summary |

---

## 9. Slant 3D design philosophy (written and secondhand sources)

**Slant 3D's own blog could not be read.** https://www.slant3d.com/blog renders "Loading…" with no posts in a static fetch. The items below come from the video and from third-party write-ups of other Slant videos.

| Principle | Value / rule | Source URL | Tag |
|---|---|---|---|
| Tolerance-agnostic joints | Replace fixed-clearance fits with features that self-center, wedge or flex: "If you're tweaking slicer settings, you're not designing a product. You are being an artisan." | Video (0:14, 23:44, 31:28) | Video |
| No supports | Orient each part and angle and chamfer features so no supports are needed. Angle small tabs and chamfer their undersides. | Video; 3printr summary https://www.3printr.com/how-to-design-overhanging-3d-printed-parts-without-support-structures-0868350/ | Video + Search-summary |
| Chamfer over fillet for downward faces | A **45°** chamfer is a "consistent overhang" (video, primary). A 3printr summary reports Slant citing **30°** as ideal for bottom chamfers, and does not say which axis that angle is measured from. Treat the video's 45° as authoritative. Prusa agrees that bed-facing fillets create steep overhangs. | Video D1 (18:28); https://www.3printr.com/how-to-avoid-rounding-on-the-underside-of-parts-during-3d-printing-2067956/ ; Prusa KB | Video + Search-summary + Primary |
| Simple first layer | Keep the bed footprint simple, with a filleted square or curved shape and no thin T or fins on the bed, to avoid warping in high-warp materials | Video B2/B3/B4 | Video |
| Design for the process | Robustness to shrinkage, colour variation and machine quirks comes from rounded corners, chamfers, compliant features and grip fins | Slant video "How to design a print with better tolerances" (description mirror) https://scribe.disroot.org/comment/6109488 | Search-summary |
| Model geometry beats slicer settings | Use 0.2 mm micro-features to force solid walls instead of changing wall counts | Video E4; 3printr summary (section 7) | Video + Search-summary |
| Internal struts | Slant reports that parts became considerably stronger when internal structures were added, acting like bridge struts | https://www.3printr.com/stability-test-how-wall-thickness-affects-3d-printed-parts-1767996/ | Search-summary |

Do **not** cite the Hackaday "fins" article (https://hackaday.com/2026/09/23/forget-trees-add-fins-to-your-3d-prints-instead/) for grip fins. It covers breakaway *support* fins, which Slant also pitched, and those are a different feature.

---

## 10. Gap-by-gap fill for video2-report.md (quick lookup)

Values are defaults for PLA or PETG at 0.4 mm / 0.2 mm. Cross-references point to the tables above, and the tags there apply.

| Joint (report ID) | Default numbers to model |
|---|---|
| Diamond peg (A1) | Square peg 6–8 mm rotated 45°, length about 6–8 mm, gap 0.15–0.2 mm per side (snug, UF), 45° x 0.5 mm tip chamfer, peg printed lying flat. Peg size UNSOURCED. |
| Slab and slot (A2) | Slab 2–3 mm thick (≥ 4 perimeters), gap 0.2 mm per side, rounded and tapered tip with 1–2° wedge taper. |
| S-bracket (A3) | Strip t = 1.35–1.8 mm, b ≥ 5 mm. Hook undercut 0.8–1.0 mm, α = 30°, α′ = 90° permanent or 45° removable. Interference ("compression") 0.3–0.5 mm. Root and bend radius ≥ 0.6t. Print flat. |
| C-clamp (A4) | Tines tapered 1.8 to 0.9 mm, L from section 1.1 (about 10–13 mm for PLA). Undercut 0.8 mm per tine, α 30°, α′ 45° for a releasable clamp. |
| Tongue / T-slot (B1, B2) | Gap 0.2–0.3 mm per side, 45° x 0.5–1 mm chamfers, EFC 0.2 mm plus 45° bed-edge chamfers. |
| Flexible T-slot (B3) | Flanges 0.9–1.35 mm thick, preload 0.3–0.5 mm, flange L ≥ 7 mm (PETG at 1% sustained strain), slot tilted 20–30°, neck gap 0.2–0.3 mm per side. |
| Eye slot (B4) | Ø20 mm eye in a 25 mm block (stated). Gap 0.2 mm per side, neck about 5 mm wide with 0.2–0.3 mm per side. |
| Grip fins (B5) | 8–16 fins, 30–45° lean, 0.3–0.5 mm radial interference, roof gap ≥ 0.4 mm. PETG (preferred): t = 0.45 mm with free length 4.5–6 mm, or t = 0.9 mm with 6.3–8.2 mm. PLA: t = 0.45 mm only, with free length 6.3–8.2 mm. |
| Locking tab (B6) | Section 1.1 worked example: t 1.8 to 0.9 mm, L about 10.5 mm (PLA), undercut 0.8 mm, α 30°, α′ 45° for bi-directional or 90° permanent, flange undersides ≤ 45° from vertical, root R about 1.1 mm. |
| Glue pad (C1) | 0.5 mm deep pockets, ≥ 0.9 mm opening, 10–20° undercut taper, 2–3 mm pitch. |
| Glue channels (C3) | Ø1.5–2 mm for CA, Ø2.5–4 mm for epoxy or hot glue, teardrop if horizontal, vent at the far end. |
| Horizontal pin (D1–D4) | 45° teardrop hole, 45° tip chamfer, 0.25 mm diametral clearance (0.125 per side), 1–2° wedge on tabs. |
| Forked pin (D5) | Prongs ≥ 0.9 mm (2 perimeters), slot between prongs ≥ 2 x bump height, bump 0.3–0.5 mm, α = α′ ≈ 30–45°, profile printed in XY. |
| Vertical pin (E2) | Ø ≥ 5 mm, L/d ≤ 1–1.5, base fillet 0.5–1 mm, tip round or chamfer 0.5–1 mm, hole 0.25 mm (to 0.5 mm) diametral oversize plus a lead-in funnel. |
| Cross pin (E3) | Height 10 mm and 1.5° draft (panel values), arms 1.35–2 mm thick, 0.25 mm diametral clearance. |
| Fluted pin (E4) | 0.2 mm slots spaced about 1 mm, running through the pin root and 2–5 mm into the body, never narrower than 0.1 mm (the slicer closes it); 0.2 mm is the tested width. Flute count about 16 (ESTIMATED from the video). |

## Open items (could not be sourced)

- BASF Snap-Fit Design Manual allowable-strain table (p. IV-4) and its U/L-shaped beam formulas (pp. V-1 to V-4). Only BASF's sponsored articles were reachable. The Covestro PDF text layer is font-encoded, and its readable table rows list only PC and PC-blend grades.
- A measured permissible strain for **printed** PLA, PETG, ABS, ASA or nylon in snap-fit service. Every material strain in this file is DERIVED from datasheet yield and break values with Bayer's molded-plastics rules.
- A same-on-same friction coefficient for PLA or PETG.
- Peer-reviewed print-in-place clearance data by orientation. The available sources are vendor and practitioner reports.
- An FDM-specific dovetail flank angle and glue-pocket geometry.
