---
name: atelier-standard
description: Design and engineering standard for building any interactive product — app, game, prototype, or interface — to the level of craftsmanship of haute couture, Rolls-Royce, and independent watchmaking, fused with rigorous, rightsized software engineering discipline. Consult before designing or building any new UI, app, game, or interactive prototype; before naming any feature, screen, or system; before writing any copy a user will read; and before declaring any build "done." Establishes the palette-lock, naming, motion, empty-state, and hidden-surface finishing standards proven on the Marks & Fate and AURELIA projects, plus the rightsized engineering discipline behind them. Trigger whenever the user asks for something to feel premium, feel finished, feel expensive, be beautiful, be built with craftsmanship, or references Rolls-Royce, haute couture, Philippe Dufour, or similar benchmarks — even if they don't name this skill directly.
compatibility: Any Claude surface — claude.ai (upload as a custom skill if your workspace allows it), Claude Code (place in a project's or personal skills directory), Cowork, Claude Desktop. A design and engineering standard, not a file-format skill — no tool dependencies.
---

# The Atelier Standard

This is not a mood board. Every principle below was extracted from two real, working pieces of software — Marks & Fate, a five-realm strategy game universe, and AURELIA, an AI-council application for exploring life decisions — cross-checked against three traditions that have spent centuries defining what "unparalleled" actually means in practice: haute couture, Rolls-Royce, and the watchmaking of Philippe Dufour.

This skill covers the **standard of output** — what the thing must feel like and how carefully it must be made. It is a companion to any project-agnostic *process* methodology already in play (build one thing fully, extract the system from the instance, lock architecture before scaling, ship in modular pieces) — that's a different axis and isn't repeated here. This is about the bar the output has to clear, at every scale, including a solo developer with an AI collaborator and no studio.

## The Lineage

Two products, three traditions. The products prove these principles survive contact with a real build at the scale most work actually happens at — one person, an AI collaborator, no funding round, often no backend at all. The traditions supply the vocabulary, each contributing something distinct, not a blurred idea of "luxury":

- **Haute couture** governs fit and hidden craftsmanship — the inside of the garment finished as carefully as the outside.
- **Rolls-Royce** governs the disappearance of mechanism behind an experience of effortlessness — complexity engineered out, not decorated over.
- **Philippe Dufour** governs the standard held where no one will ever check — and is the single most relevant reference of the three, because his entire body of work is proof that mastery has never required scale.

Full grounding for each, and exactly what it translates to, lives in `references/craftsmanship-lineage.md`. Line-level worked examples from both real products live in `references/case-studies.md`. The rightsized engineering argument — what a studio-scale blueprint actually protects and what protects the same thing solo — lives in `references/engineering-discipline.md`.

## The Standard

### 1. Naming & Voice

Nothing generic ships. Every screen, state, currency, and character gets a name that belongs to the world being built, chosen before the feature is built around it — never applied afterward as flavor text.

- No "levels" — Realms. No "AI difficulty" — three named spirits whose lore evolves with the player's history against them.
- No "menu" — a Vestibule, an Observatory, a Vault, an Archive. No "AI-generated scenarios" — a six-member Council, each member with one defined role.
- Empty and error states are not afterthoughts. "No futures have been summoned yet. The Vault holds what the Observatory generates" does more work, in-voice, than "No items found." Write these with the same care as the headline copy — they are usually the second-most-viewed screen in any product.
- A raw mechanic exposed to the user — a difficulty slider, a JSON key, a toggle labeled after its variable name — is an unfinished decision, not a neutral one. If it can be a character, a place, or a ritual instead, it should be.

### 2. The Visual System

One palette. One accent. Locked before the first screen is built, never diluted under deadline pressure.

- A single dark base, a single precious accent color, one serif carrying every headline across an entire universe of otherwise-unrelated screens.
- Typography can be assigned semantic roles, not just picked: one face for anything emotional or voiced, one for reading, one for anything institutional or systemic — labels, status text, eyebrows. Each face gets exactly one job and never does another one.
- Motion runs on a single locked easing curve, defined once as a variable, referenced everywhere. Never hand-tune a transition in isolation.
- Native browser affordances get re-skinned, not ignored: text selection color, focus rings, scrollbar thumbs. Leaving these at browser defaults is a couture gown with a polyester lining — nobody misses it until they see one that doesn't have it.
- `prefers-reduced-motion` is checked and respected as a first-class code path, not a nice-to-have. This is the accessibility-as-luxury principle translated directly into code.

### 3. Mechanism Behind Calm

The Rolls-Royce instinct: an engine's complexity exists so the passenger never has to think about it.

- **Dress the mechanism as character, never expose it as a setting.** A minimax search at depth five is "a spirit who reads all possible futures." A structured API call returning ranked JSON is "the Council deliberates." The engineering underneath should be as rigorous as the metaphor is calm — this is not about hiding weak implementation behind pretty words, it's about never making the user read the implementation to enjoy the result.
- **Decouple pacing from raw latency — ceremony pacing.** If an interaction is meant to feel considered, hold its animation to a fixed minimum duration regardless of how fast the underlying response actually arrives (`Promise.all([doWork(), minWait])` is the pattern). An instant reply reads as thin, not efficient, when the interaction is supposed to feel weighty.
- **State the outcome, not the spec.** Never show "Difficulty: Hard (search depth 5)." Show what the character does. Understatement is not the absence of information — it's information deliberately withheld from the surface and kept correct underneath.

### 4. The Hidden Surface — Dufour's Rule

Philippe Dufour hand-bevels and mirror-polishes the internal angles of a movement that will be cased and never seen again by anyone, including its owner, for the rest of its life. He does this work anyway, because the standard is not "good enough to pass inspection" — there is no inspection. The standard is what the maker can privately stand behind.

The direct translation: hold code, logic, and content that no user will ever consciously notice to the exact same standard as what's on screen. Decorative elements can be built on genuinely correct underlying math instead of approximation, purely because it's more correct, with zero expectation anyone will ever verify it. Rules logic gets audited for actual correctness, not just plausibility — a bug that no player would ever file a report about is still a bug, and gets fixed anyway. This extends to error handling nobody will trigger on a good day and edge cases in code that will very likely never run. Build them as if they will.

### 5. Engineering Rigor, Rightsized

The instinct that actually transfers from large-scale engineering blueprints to solo, AI-assisted work is never a specific technology choice — it's first-principles scoping applied honestly at the scale the work is really happening at.

- **Question the requirement before honoring it.** A solved problem with no ceiling doesn't deserve an elaborate system built around it, no matter how polished the wrapper. The first, hardest, most valuable move is sometimes refusing the brief as given.
- **Delete before you optimize.** If a mechanic, screen, or system doesn't serve the one feeling the product is built around, cut it — including things you're already attached to.
- **The AI–human relationship is adversarial by design, not polite by default.** Real progress comes from the AI critiquing the human's first idea, and from the human refusing to accept the AI's own account of its work at face value. Neither party gets the last unchallenged word. Build this in deliberately: invite critique before building, and audit anything reported as "done" by actually opening it — not by re-reading the summary of it.
- **Match infrastructure to actual scale, not aspirational scale.** A distributed backend protects state at massive concurrent scale; a single, exactly-documented data schema that every file reads and writes identically protects the same thing at the scale of one developer and no backend. Importing infrastructure a project doesn't need isn't rigor — it's cargo-culting rigor's aesthetic without its substance.
- **Report status honestly, including your own mistakes.** If a claim of "done" turns out to be wrong, that gets corrected on the record, not quietly patched — so the next session can see that the gap existed and how it was caught, not just the after-picture.

## Before You Say "Done"

A status report is a hypothesis about reality, not a fact — including one generated by an AI, including one generated a moment ago. Before declaring a build, a feature, or a document complete:

- Open the actual files. Don't trust a summary of what they contain.
- Exercise the actual thing through every terminal state — not just the happy path once.
- Re-read any document making completion claims against the real file list, not against memory of what was intended.
- If something was designed twice in conversation but never saved as a working file, it is not built. A polished description is not an artifact.

This checklist exists because exactly these failures happened once on a real project in this lineage, were caught by one direct question, and were fixed in the same session they were found. Treat that as the standard, not the exception.

## Where to Go Deeper

- `references/craftsmanship-lineage.md` — full grounding in haute couture, Rolls-Royce, and Philippe Dufour's specific techniques and philosophy, and exactly what each translates to in software.
- `references/case-studies.md` — line-level worked examples: palette locks, naming systems, ceremony-pacing code, a genuine Fibonacci sphere used for decoration, a real rules bug caught while re-implementing a game.
- `references/engineering-discipline.md` — the full rightsizing argument: what a studio-scale engineering blueprint actually protects, mechanism by mechanism, and what the equivalent discipline looks like with one developer and an AI instead of a large team and a cloud budget.
