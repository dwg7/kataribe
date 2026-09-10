# kataribe (語り部)

**A dossier-based narrative Staff for the Staccato architecture.** A 語り部 (kataribe) is, in Japanese, someone who carries a memory forward across generations, retelling it in the form each listener needs — a war's kataribe, a disaster's kataribe. This repository builds a Staff that does the same thing for a place: hold one well-verified, versioned account of what happened there, and retell it — thinly, honestly, in the right register — for whoever is actually asking, right now, for their own reason.

## What this is, concretely

A Staff whose core behavior is: given a **dossier** (a pre-authored, fact-checked, versioned account of one real event tied to one real place), recognize which of that event's several genuine layers of significance — hazard, livelihood, place-identity, and others — the current asker actually needs, and present only that layer, adapted to their register, without originating new facts on the fly.

This is deliberately **not** a general-purpose conversational map assistant (that's [`dwg7/chukei`](https://github.com/dwg7/chukei)'s job) and not a from-scratch content generator (that risk is exactly what dossiers are designed to remove). It leans on prepared material more heavily than any sibling project so far — see `CLAUDE.md` for why.

## Origin and first instance

This repository grew out of an ecosystem-strategy conversation in [`dwg7/staccato-ecosystem`](https://github.com/dwg7/staccato-ecosystem) (2026-09-05): [`dwg7/kitavolca`](https://github.com/dwg7/kitavolca) (a Hokkaido volcano data pipeline) and [`dwg7/kaga0`](https://github.com/dwg7/kaga0) (an air-gapped Cartographer appliance) were identified as mature Library/Cartographer-side work with no matching Staff — a genuine, confirmed gap. A first design proposal (drafted by a `model: fable` subagent, reviewed by hfu) narrowed this further, to its smallest real starting point: a Staff that can competently retell **十勝岳大正泥流** (the Taisho-era mudflow disaster at Mt. Tokachi, 1926-05-24) — chosen partly because 2026 is its 100th anniversary, and partly because the event itself is a near-perfect illustration of layered significance: the same land is simultaneously a hazard site and, today, farmland — disaster and livelihood are literally the same physical deposit, at different points in time.

The repository is intentionally **general-purpose** — not scoped to volcanoes, and not scoped to Hokkaido — even though its first dossier is. See `HANDOVER.md` for the current state and the raw source material for that first dossier.

## Relationship to sibling repos

- [`dwg7/staccato-ecosystem`](https://github.com/dwg7/staccato-ecosystem) — the methodology this Staff draws on (the collaboration-planning process, the "誰が最終利用者か" and multi-stakeholder patterns) and the place where the layer-recognition-and-selection design pattern this repo tests should eventually be written up, once proven here.
- [`UNopenGIS/staccato-spec`](https://github.com/UNopenGIS/staccato-spec) — the normative Staff/Cartographer/Library architecture (ADR 0001's Faceless Cartographer, human-mediated handoff, is part of why this design treats verification as cheap-by-construction — see `CLAUDE.md`).
- [`dwg7/kitavolca`](https://github.com/dwg7/kitavolca) — the Library this Staff's map links resolve against (VBM/VLCM Hokkaido volcano data, served via `stars.optgeo.org`).
- [`dwg7/kaga0`](https://github.com/dwg7/kaga0) — an air-gapped Cartographer appliance; a plausible future deployment target, not the first one.
- [`dwg7/spiccato`](https://github.com/dwg7/spiccato) — the Cartographer this repo's dossier links actually resolve against, chosen 2026-09-05 (`DECISIONS.md` D3): its single-Map-Intent-per-link `#q=` model matches kataribe's "one question → one selected layer → one resolved render" shape exactly, and it already carries kitavolca's volcano data in its live catalog.
- [`dwg7/ferspas57`](https://github.com/dwg7/ferspas57) — a sibling Staff built on the same "select from pre-authored material, adapt language live, never generate content" principle, and the source of the multi-step narrative mechanism kataribe deliberately did *not* need for its first dossier. Reserved for a future dossier layer that genuinely needs an internal step-by-step build-up. See `DECISIONS.md` D3.
- [`dwg7/chukei`](https://github.com/dwg7/chukei) — the general-purpose GSI Hokkaido Staff this project is a sibling to, not an extension of. Kataribe does not embed chukei's full capability.

## Status

Early, but no longer scaffold-only. As of 2026-09-11 the repository holds a first dossier ([`dossiers/tokachidake-taisho-mudflow-1926.json`](dossiers/tokachidake-taisho-mudflow-1926.json) — hazard and place-identity layers fact-complete, livelihood layer deliberately marked incomplete rather than padded), the dossier schema ([`DOSSIER-FORMAT.md`](DOSSIER-FORMAT.md)), and a first draft of the Staff prompt itself ([`STAFF-PROMPT.md`](STAFF-PROMPT.md)).

The Staff prompt is written but **not yet validated against real questions** — that is the next task. See [`HANDOVER.md`](HANDOVER.md) for current state and [`DECISIONS.md`](DECISIONS.md) for the reasoning behind each design call.

## License

[CC0 1.0 Universal](LICENSE) for this repository's own code and prose. Note: the first dossier draws on a copyrighted GSI publication (see `HANDOVER.md`) — used under Japan's government standard terms of use and hfu's own existing usage approval, treated as citation/adaptation of the underlying facts rather than reproduction of GSI's own document.
