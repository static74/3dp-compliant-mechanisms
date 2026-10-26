# Plan: 3dp-compliant-mechanisms skill, adversarial content review
_Round 1 — revised by Claude after Codex round 1 (see PLAN-REVIEW-LOG.md for the 17 findings and responses). The skill files themselves were edited; this brief is unchanged except this line._

## Goal
The artifact under review is a Claude skill, not code: `skill/SKILL.md` (router) plus `skill/references/*.md` (one file per mechanism family). It teaches Claude to design compliant mechanisms and tolerance-free joints for FDM printing using Slant 3D's method, with every dimension tagged by provenance (`[video]`, `[measured]`, `[source: URL]`, `[judgment]`). Three eval prompts were run with and without the skill; the answers are in `docs/eval-runs/` (with-skill files have no suffix, baselines end in `-baseline.md`). The review question: will an engineer who follows this skill produce parts that print and work, and is anything in it wrong, internally inconsistent, unsafe to print, or missing for the mechanisms it claims to cover?

## Approach (what to read, in order)
1. `skill/SKILL.md` — selection table, binding spring rule, workflow.
2. `skill/references/fundamentals.md` — strain table, formulas, clearances, first layer, micro-slots.
3. `skill/references/compliant-lids.md`, `snap-fits.md`, `tongue-and-slot.md`, `pins-and-holes.md`, `spring-loaded.md`, `spring-capture.md`, `glue-features.md`.
4. `docs/eval-runs/2026-10-26-*.md` — judge whether the with-skill answers are buildable and whether the baseline answers expose anything the skill should have taught but did not.
5. `docs/research/*.md` only if you need to check a number's source.

## Key decisions & tradeoffs (bite here)
- Strain limits are derived from moulded-plastic snap-fit rules (Bayer) applied to printed-filament datasheet yield strains, not measured on printed beams. PLA 2.0/1.2/0.5 %, PETG 3.6/2.1/1.0 % (single/repeated/sustained).
- Two fin recipes coexist in compliant-lids.md: Slant's measured part (1.27 mm fins, 1.9 mm pitch, 65° to wall) and a strain-safe default (0.86 mm, 2.5–3 mm pitch, 30–45°, L ≥ 9.5–10.5 mm). The skill offers both.
- Relief gap under flexures is 0.3 mm, justified by mid-layer slicing; video 1 modelled 0.2.
- Metal springs are captured only by (A) one-way barbed plunger or (B) slicer pause; the catch face is 90° and never chamfered even when it is a downward overhang.
- Thickness quantisation to perimeter multiples (0.45/0.9/1.35/1.8) and the 0.2 mm micro-slot trick rely on PrusaSlicer behaviour; other slicers are assumed similar.
- Clearance convention is per side everywhere except the video's 0.25 mm diametral pin rule.

## Risks / open questions
- Formula consistency: 0.67 vs 1.09 (tapered) vs 1.5·y·t/L² forms appear in different files; check that each use is correct and that no file mixes them.
- Barbed plunger on a Ø6 part: are prong thickness, slot, barb height and counterbore mutually consistent?
- Does any recipe produce an unprintable overhang, a sub-nozzle feature, or a Z-direction flexure?
- Are the eval assertions discriminating, or could a wrong answer pass?

## Out of scope
Rewriting the videos' claims; resin/MJF; CAD file generation; test prints (none have been made).
