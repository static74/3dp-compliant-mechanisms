# Decisions

## 2026-10-26 Skill is a router plus per-family reference files

Question: one long SKILL.md or a thin SKILL.md with references?

Decision: thin router. SKILL.md holds the selection table, shared FDM rules and the spring-capture choice. Each mechanism family has its own file under `skill/references/`. Claude loads only the family it needs, and a new technique is one new file plus one table row.

Rejected: a single document. It would pass 1,500 lines on day one and every session would pay for all of it.

## 2026-10-26 Every number carries provenance

Question: present the video-derived estimates as specs?

Decision: no. Both source videos (Slant 3D lids and joints guides) state almost no dimensions. Values are tagged `[video]`, `[measured]`, `[source: URL]` or `[judgment]` so a user can tell a stated 0.25 mm pin clearance from a frame-measured fin thickness.

Rejected: untagged "recommended values". They would read as tested when they are not.

## 2026-10-26 Spring-loaded mechanisms offer printed or metal spring

Question: how does a plunger keep a metal spring captive?

Decision: two documented options, both required by the brief. Option A: one-way barbed plunger (cantilever ears, insertion ramp, 90° retention face) that snaps into the bore from outside and cannot be ejected by the spring. Option B: slicer pause (M601 / pause-at-height) at the cavity roof so the spring is placed mid-print and sealed in. The printed-spring path (serpentine or cantilever leaf, flexing in the XY plane) is the default when travel under about 2 mm is enough.

## 2026-10-26 First eval pass drove six fixes

Question: did the skill produce usable designs on realistic prompts?

Two with-skill runs (grip-fin lid for a 60 × 40 enclosure; barbed PETG plunger with a pen spring) both followed the routing and output format and produced buildable parameter tables; outputs are in `docs/eval-runs/`. Their feedback added: a fin pitch/count/length scaling formula, a box-wall minimum, interference tied to material, rigid-base guidance, pen-spring measurement and cut-to-rate guidance, rotary detent nose geometry, neck-bore vs counterbore terminology, a small-plunger prong note, flat-chord rule, and a pointer to where `docs/research` lives. No baseline (without-skill) runs or graded benchmark were made; the three eval cases under `skill/evals/` are ready for `claude plugin eval`.
