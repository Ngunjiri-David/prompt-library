# Case Studies — Worked Examples

Two real products, examined for what they actually did, not what they claim to do. Use these as direct precedent when a new build needs to decide "what does the standard look like in code."

---

## Side-by-side: the same five principles, two different products

| Principle | Marks & Fate | AURELIA |
|---|---|---|
| Locked palette | Near-black `#0F0D0B` base, single warm amber accent (`#C4923A`), held identical across five separate games | Obsidian `#0A0A0A` base, graphite secondary, single gold accent (`#C7A56A`), held identical across four "spaces" |
| Typography role assignment | One serif (Cormorant Garamond) for every headline, everywhere | Three faces, three jobs: Fraunces (serif) for anything emotional/voiced, Inter weight-300 for body reading, IBM Plex Mono for anything institutional — labels, status, eyebrows |
| Naming discipline | "Realms" not levels; "Seeker rank" not player level; "Fate Points" not currency; three named spirit opponents instead of exposed AI-difficulty settings | "Vestibule / Observatory / Vault / Archive" not menu/game/shop/history; a six-member named Council instead of an exposed model-call |
| Mechanism dressed as character | A minimax search at configurable depth is "The Fate Weaver — she reads all possible futures," with lore text that changes at 0, 1–4, and 5+ cumulative wins | A single structured API call returning three ranked JSON objects is "the Council deliberates," staffed by six named, individually-defined personas (Architect, Skeptic, Economist, Historian, Oracle, Shadow) baked into the system prompt |
| Ceremony pacing | AI opponent "thinking" delay scales with difficulty (700ms easy → 1450ms hard) via `setTimeout`, so a move never appears instantaneously regardless of how fast the calculation actually was | Question-to-answer flow holds a "fracture" animation to a fixed 1700ms minimum via `Promise.all([generateFutures(q), minWait])`, so a fast API response never truncates the ritual |
| Hidden-surface correctness | A rules bug (4 of 16 valid mill lines missing from the win-detection logic) was found and fixed while re-implementing a board — no player would have filed this as a bug report | A starfield/sphere background uses a genuine Fibonacci-sphere point distribution (`phi = acos(1 - 2*(i+0.5)/N)`, golden-angle theta) for even point spacing — correct math for a detail no user will ever consciously evaluate |
| Empty/error states in-voice | Locked screens show FP progress toward unlock rather than a bare padlock icon; legal/compliance copy is written in full sentences, not boilerplate | "No futures have been summoned yet. The Vault holds what the Observatory generates." / "The Council could not be reached. Ask again." — both replace generic empty/error copy entirely |
| Native affordances re-skinned | Custom scrollbar thumb color matched to the palette across every screen | `::selection` background and `:focus-visible` outline both re-skinned to the gold accent instead of left at browser default blue |
| Accessibility as a real code path | High-contrast-friendly palette choices throughout | `prefers-reduced-motion` explicitly detected once (`window.matchMedia`), applied as a body class, and every keyframe/transition in the stylesheet collapses to near-zero duration when set |
| Local-first data discipline | One documented schema (`mf_save`) read and written identically by every realm file — no parallel formats permitted | `window.storage` used with explicit `try/catch` around every call, defaulting gracefully to an empty array rather than throwing when nothing has been saved yet |

---

## Detail: ceremony pacing, in code

The pattern, generalized from AURELIA's implementation:

```javascript
const MIN_CEREMONY_MS = 1700;
async function doRitualAction(payload) {
  const minWait = new Promise(res => setTimeout(res, MIN_CEREMONY_MS));
  const [result] = await Promise.all([ doRealWork(payload), minWait ]);
  return result; // never resolves before the ceremony has visually finished,
                  // regardless of how fast doRealWork() actually was
}
```

The point isn't to add artificial latency for its own sake — it's that when an interaction is *designed* to feel weighty (a spirit "considering" a move, a Council "deliberating"), the pacing of that feeling should be authored on purpose, not left as an accident of network speed. A 40ms API response finishing a "the Council deliberates" animation instantly reads as broken, not fast.

## Detail: the hidden-surface bug, as a template for auditing

What happened: a board game's win-detection logic was ported from an earlier prototype into a production file. While rebuilding it line by line (not just copying it), the mill-detection array was checked against the actual rules of the game rather than assumed correct because it had "always worked." It was missing four of sixteen valid mill combinations — the four that ran through the board's connecting "spoke" lines rather than its concentric squares. No playtest had surfaced this because those four lines were rarely the ones a casual player or a simple AI happened to complete.

The general lesson, not specific to this bug: when re-implementing something that already "works," re-derive correctness from the actual specification, don't just carry the old logic forward on the assumption that prior use would have caught a flaw. Absence of complaints is not evidence of correctness — it's often just evidence that the flawed path is rarely taken.

## Detail: naming a mechanic into a character

Before → after, as a repeatable move:

1. Identify the raw mechanic (a difficulty enum, a model call, a database write).
2. Ask what it would be called if it were a person, place, or ritual inside the world already being built.
3. Give it a one-line identity — not just a label, an actual defined role or personality trait.
4. Let that identity's presentation evolve with state (win count, time elapsed, data accumulated) so it isn't just a static reskin.

Marks & Fate's spirits: `easy | medium | hard` → Iron Shaman / Forest Wraith / Fate Weaver, each with three tiers of lore text keyed to cumulative wins against them.
AURELIA's Council: one Claude API call with a JSON schema → six named personas with one defined role each, listed in the loading state so the "deliberation" has visible, named participants before the answer ever arrives.
