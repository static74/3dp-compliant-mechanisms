# Agent rules for this repo

This repo is a Claude skill. The skill itself lives in `skill/` (SKILL.md plus `references/`). Everything outside `skill/` is repo plumbing and documentation.

- Edit mechanism knowledge in `skill/references/<family>.md`, not in SKILL.md. SKILL.md is the router: when to use which mechanism, the shared FDM rules, and the spring-capture decision. Keep it under 300 lines.
- Every number in a reference carries a provenance tag: `[video]` (stated in a Slant 3D video), `[measured]` (read from video frames, with the scale used), `[source: URL]` (published guide), or `[judgment]` (engineering judgment, untested). Never strip tags; a future printer test may overturn a `[judgment]` value.
- Adding a mechanism: copy `skill/references/_template.md`, fill every section, add one row to the selection table in SKILL.md, add an eval case under `skill/evals/`. Record the addition in `docs/decisions.md`.
- Tests are the eval cases in `skill/evals/`. Run with `claude plugin eval skill --allow-tools Write,Edit,Bash` from the repo root.

Docs map: `docs/decisions.md` (dated ADRs), `docs/sources.md` (videos and guides the numbers came from).
