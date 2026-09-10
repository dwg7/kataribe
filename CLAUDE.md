# kataribe — Project Context

Persistent context for Claude Code sessions working in this repository (`dwg7/kataribe`, cloned at `/Users/hfu/kataribe`). If a session starts here, read this file, then read `HANDOVER.md` for the current status.

**Language convention**: English for meta-documentation (this file, `README.md`, `DECISIONS.md`, `HANDOVER.md`), matching the general `dwg7` pattern. Chat with hfu happens in Japanese regardless. Dossier content itself (facts, sources) should be written so it can be adapted into other languages live by whichever Staff/host reads it — see "What kataribe reuses from ferspas57" below; don't pre-translate dossiers into multiple languages.

## What this project is

A Staff whose core behavior is: given a **dossier** (a pre-authored, fact-checked, versioned account of one real event tied to one real place), recognize which of that event's several genuine, simultaneous layers of significance (hazard, livelihood, place-identity, and others — none more "real" than another) a specific asker actually needs right now, and present only that layer — thinly, honestly, adapted to their register — without originating new facts on the fly. Named after 語り部 (kataribe): someone who carries a memory forward across generations, retelling it differently for whoever is listening.

**Founding motivation**: an ecosystem-strategy conversation in `dwg7/staccato-ecosystem` (2026-09-05) identified `dwg7/kitavolca` (Hokkaido volcano data pipeline) and `dwg7/kaga0` (air-gapped Cartographer appliance) as mature Library/Cartographer-side work with no matching Staff — a real, confirmed gap (checked directly with kitavolca's own session). A design proposal (drafted by a `model: fable` subagent, reviewed by hfu) narrowed this to the smallest real starting point: a Staff that can competently retell **十勝岳大正泥流** (the 1926-05-24 Tokachidake mudflow disaster — 2026 is its 100th anniversary). See `HANDOVER.md` for the primary-source material already gathered for that dossier.

**hfu's explicit framing for why this repo exists and is shaped this way**:
- The repo is **general-purpose**, not volcano-specific — hence the name, deliberately not something like "volkataribe." The first dossier happens to be about a volcano; the pattern (one dossier, many layers, recognize which one a specific asker needs) is not.
- This leans on prepared material even more heavily than `dwg7/ferspas57` did — see "Constraint approach" below.
- Societal skepticism toward generative AI ("it can be wrong") is this project's ally, not a headwind: unlike freeform AI prose, this Staff's output (a dossier citation, a real map link) is cheap to verify — open it and look, don't just trust it. See `dwg7/staccato-ecosystem`'s `methodology/responsibility-sharing.ja.md` for the fuller argument; lean into this positioning rather than treating honesty about fallibility as merely defensive.

## The three core design calls (from the Fable-drafted proposal, reviewed by hfu)

1. **Audience, v1: local intermediaries only** — municipal disaster-prevention staff, teachers, tourism/onsen operators, community leaders. Not GSI-internal staff (`dwg7/chukei`'s job), not the general public directly. Framed as strengthening the accountable human chain (an intermediary reviews before passing on), not liability avoidance — this is also `responsibility-sharing.ja.md`'s shared-responsibility principle in architectural form.
2. **The significance a place/event carries is multi-layered, and Staff's job is recognition-and-selection, not fixed-theme coverage.** For 十勝岳大正泥流 specifically: hazard (the mudflow itself, the 25–26 minute reach time, the 144 dead/missing), livelihood/agriculture (the same deposit is today's farmland near Kamifurano — literally the same land, different point in time), place-identity (why this stretch of the Furano basin looks the way it does), and likely others as more dossiers accumulate. **Not yet promoted to a `staccato-ecosystem` methodology principle** — validate it here first (this repo's whole first dossier is effectively a test of whether recognition-and-selection actually works in practice), then propose generalizing once proven, not before.
3. **Constraint approach: "lowering the bar" (dossiers) is primary, "embedding" is secondary and minimized.** All per-event content is pre-authored and versioned; Staff selects and adapts register/language live, never originates facts. This project leans on this *even more* than `ferspas57` did (hfu's own read, 2026-09-05) — the domain is safety-adjacent, and dossiers are effectively mandatory for any no-internet host anyway. Embedding (chukei-style, physically including the map-link-building capability) is needed only for a Gennai-hosted packaging, and even then, this Staff should not embed chukei's full general-purpose capability — it's a sibling, not an extension.

## Dossier sourcing and copyright

The first dossier draws on GSI's official 1:50,000 火山土地条件図「十勝岳」explanatory document (published 1990, the map's own printed notice says "許可なく複製を禁ずる"). hfu confirmed (2026-09-05): Japan's government standard terms of use partially supersede that older printed notice, and hfu already holds his own usage approval (as with `kitavolca`'s 測量法 approval) — so this is a lower-risk situation than the printed notice alone suggests. Even so, **treat this and any future GSI/official source as citation and adaptation of the underlying facts, not reproduction of the source document's own text, images, or layout.** Always record the source and its usage basis in the dossier file itself (mirroring `kitavolca`'s attribution-in-metadata practice).

## What kataribe reuses from ferspas57 (verified 2026-09-05, don't assume more than this)

`dwg7/ferspas57`'s `docs/story.js` (as actually pushed to `main` as of 2026-09-05 — **not** the more advanced `narrative.js`/English-only/live-register-adaptation redesign described in that repo's own working notes, which exists only in another session's local files and has not been pushed to any branch there yet; don't assume it exists until verified again) implements: a narrative as a JSON script (`{title, steps: [{center, zoom, layers, caption}, ...]}`), played via `flyTo` + synced layer checkboxes + a caption panel, handed off through a URL fragment (`#story=`) using `LZString` compression, and — importantly — a **one-shot, ADR-0004-compliant fragment read-and-clear** (`readAndClearFragmentKey`, shared across every fragment-carried key that Cartographer accepts) so a copied URL is never itself replayable/bookmarkable map state.

**Reuse the mechanism, not the schema as a fixed contract.** hfu's explicit read (2026-09-05): since ferspas57's own narrative format is itself still mid-revision and not yet settled/pushed, kataribe has real discretion to shape its own dossier/narrative JSON structure to fit the layer-recognition-and-selection need (which is a different shape from ferspas57's linear multi-step flyTo story — a dossier's "steps" are more like "one per layer," selected rather than sequenced) — this isn't a schema kataribe is locked into replicating. What's worth forking/keeping as-is: the `flyTo`+layer-sync+caption playback mechanism, the fragment-based one-shot handoff (`readAndClearFragmentKey`), and the general shape of "Staff selects/adapts, never originates facts live" (whichever of ferspas57's two narrative-authorship designs — 10-language pre-baked, or English-only-plus-live-adaptation — turns out to be current when you check, the *latter* is very likely the better model to follow here, precisely because it doesn't require re-authoring a dossier per language up front; verify ferspas57's actual current state before committing to either).

## Relationship to sibling repos

- **`dwg7/staccato-ecosystem`** — the methodology this Staff draws on (collaboration-planning process, the 最終利用者/展開する立場 distinction, multi-stakeholder patterns) and the destination for the layer-recognition-and-selection pattern once validated here, not before.
- **`UNopenGIS/staccato-spec`** — the normative architecture. ADR 0001 (Faceless Cartographer, human-mediated Staff→Cartographer handoff) and ADR 0004 (one-shot fragment handoff) both matter directly here — the latter because this Cartographer's narrative playback depends on it.
- **`dwg7/kitavolca`** — the Library this Staff's map links resolve against (VBM/VLCM Hokkaido volcano data via `stars.optgeo.org`).
- **`dwg7/kaga0`** — an air-gapped Cartographer appliance; a plausible future deployment target, not the first one.
- **`dwg7/ferspas57`** — source of the Cartographer mechanism to fork/adapt (see above). Check its actual current state before assuming which narrative-authorship design is live.
- **`dwg7/chukei`** — the general-purpose GSI Hokkaido Staff this project is a sibling to, not an extension of.

## Continuity files

- `HANDOVER.md` — current state, the primary-source material gathered for the first dossier, and the immediate next task. **Read this first in any new session.**
- `DECISIONS.md` — ADR-lite decision log, append-only, newest at the top (matches `dwg7/chukei`'s and `dwg7/staccato-ecosystem`'s convention).
