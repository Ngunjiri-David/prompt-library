# Engineering Discipline, Rightsized

Large-studio engineering blueprints — AAA game engines, distributed backends, twenty-person review chains — describe real discipline. The discipline is worth extracting. The infrastructure almost never is, for anyone building solo or in a small AI-assisted team with a client-only or local-first product. This file makes the mapping explicit, mechanism by mechanism, so "rigor" doesn't get confused with "adopting the same tools a much bigger team uses."

## Mechanism by mechanism

| Studio-scale mechanism | What it actually protects | The equivalent at solo, AI-assisted scale |
|---|---|---|
| AAA game engine, custom shaders, photorealistic asset pipelines | Nothing looks like a default template; every visual choice was made on purpose | A locked, zero-compromise design system — one palette, one type pairing (or one type-per-role system), one motion language — applied identically across every screen |
| Distributed backend, specialized databases, container orchestration, automated fault injection | The product doesn't silently corrupt state or fall over under real use | One documented, exact data schema that every module reads and writes identically, with the same rigor a distributed system gets — "no parallel storage format" is the same discipline as chaos engineering, applied to a single local object instead of a cluster |
| Large team with mandatory multi-person review gates | Nothing ships that only one person has scrutinized | The AI is explicitly invited to critique before building, every time; the human explicitly re-audits anything the AI reports as "done" rather than accepting the summary — this is the actual review gate, just with two participants instead of twenty |
| Extended mandatory playtesting, load testing at multiples of expected peak | Nothing ships on the strength of a demo; edge cases are found by real use, not assumed away | Play the actual build to genuine completion — every branch, every terminal state — before calling it finished; treat a written QA checklist as non-optional |
| Large hand-picked beta program, staged rollout by traffic percentage | Real, uninvolved humans encounter the product before the full audience does | A small number of genuinely uninvolved testers, taken seriously, before any public release — small doesn't mean skippable |
| Continuous deployment infrastructure, automatic self-healing | The system scales and recovers without manual heroics | Modular files instead of one monolith, so growth never requires rebuilding what already works |

## What this does NOT license

The table above is a translation, not a permission slip to reach for smaller versions of the same tools regardless of need. Specifically, do not import the following into a client-only or local-first project on the theory that it's "more rigorous":

- **A game engine or 3D rendering pipeline**, when the actual interface is 2D and fully expressible in HTML/CSS/SVG/Canvas. Adopt real-time 3D tooling only when a concept genuinely requires it, not by default.
- **A backend language/database/orchestration stack**, when the product has no multiplayer, no server-authoritative state, and no reason to leave the user's device. If a future concept genuinely needs a live backend, the right move is researching the minimal viable architecture for that specific need — not adopting a distributed-systems stack wholesale because it appeared in a blueprint once.
- **Large-team process** — mandatory multi-person sign-off, a formal QA department — when there is no team. The AI-human adversarial review loop described in the main skill file is the correct-sized replacement, not a lesser substitute to feel apologetic about.
- **Assumptions about price point or business model** carried over from a blueprint written for a different context. A premium *feel* and a premium *price* are different axes. A one-time, modest, no-dark-pattern purchase can express exactly the same "we respect you enough not to manipulate you" position a $100 price tag is meant to signal — arguably a harder version of that claim to pull off, since there's no price anchor doing persuasive work on the user's perception of quality.
- **Large-scale beta or staged-rollout infrastructure**, when five real testers, taken seriously, will surface the issues that actually matter at this scale.
- **Fault-injection or chaos-engineering tooling**, when there's no live service to inject faults into. The equivalent discipline is a written, followed QA checklist run before every release — same underlying value (verify resilience deliberately, don't assume it), sized to what's actually running.

## The test to apply before adopting any specific tool or process

Ask what the tool or process actually protects — not what it signals. If the same protection can be achieved with a simpler mechanism at the scale the project is actually operating at, use the simpler mechanism and hold it to the same rigor the complex version would have demanded. Complexity adopted for its own sake, or because a reference blueprint used it, is the opposite of the standard this skill describes — it's decoration mistaken for engineering.
