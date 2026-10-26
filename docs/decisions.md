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

## 2026-10-26 Iteration-1 benchmark: 100 % with skill vs 43 % without

Three eval cases, one run each per configuration, Sonnet. With skill 14/14 assertions at the time of the run (15 after a post-run grader was added); without skill 6/14 (43 %). The baseline answers were competent engineering (loose lip plus cantilever arms; tapered dovetail; screwed-cap plunger) but none used a preloaded compliant feature, a relief gap, provenance tags, or the barbed/pause capture rule. Cost: about +10 s and +12 k tokens per answer. Grading flagged two weak assertions (a conditional that passed vacuously, and one written for the flexible T-slot when the skill legitimately chose the grip-fin eye); both reworded. Outputs and benchmark in `docs/eval-runs/`.

## 2026-10-26 Codex (gpt-6-astra, high) adversarial review, five rounds

Question: is the skill's geometry internally consistent and buildable, judged by a second model with no stake in it?

Five read-only rounds (`docs/reviews/2026-10-26-codex-astra-log.md`). Round 1 found 17 defects, most real: plunger cavity formula erased the preload, the Ø6 prong recipe did not close, flat chord was 0.4·D instead of 0.71·D, fin depth used cos for sin, a rigid rail reconnected the fins, the snap-fit example broke its own L/t rule, sustained-strain limits were presented as sourced. Rounds 2–3 drove the plunger to a closed design (uniform Ø6, local ears, Ls + Lb = Ln + s), the lid to a sized error budget (PLA fins 13.5 mm at δ_max 0.5), the flexible T to explicit n/W/R geometry, and method B to a bayonet-cap capture with datums. Round 4 caught that an aborted edit batch had left six fixes off disk; round 5 confirmed them and left two small items, applied afterwards by Claude. The skill is materially different from the one the iteration-1 benchmark measured; that benchmark is historical only.

Rejected: dropping the two-method spring-capture rule (user requirement), and regenerating the iteration-1 eval answers (kept as history).
