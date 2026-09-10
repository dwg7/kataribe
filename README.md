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
- [`dwg7/ferspas57`](https://github.com/dwg7/ferspas57) — the Cartographer this repo expects to reuse or fork: its `docs/narrative.js`/`NARRATIVE-FORMAT.md` (a pre-authored, versioned narrative library that Staff selects from and language-adapts, rather than generates) is architecturally the same shape kataribe needs, just pointed at different data. See `CLAUDE.md` for what's expected to be shared vs. adapted.
- [`dwg7/chukei`](https://github.com/dwg7/chukei) — the general-purpose GSI Hokkaido Staff this project is a sibling to, not an extension of. Kataribe does not embed chukei's full capability.

## Status

Just founded (2026-09-05). Scaffold only — no dossier, no prompt, no Cartographer adaptation yet. See [`HANDOVER.md`](HANDOVER.md) for the immediate next task and the primary-source material already gathered for the first dossier.

## License

[CC0 1.0 Universal](LICENSE) for this repository's own code and prose. Note: the first dossier draws on a copyrighted GSI publication (see `HANDOVER.md`) — used under Japan's government standard terms of use and hfu's own existing usage approval, treated as citation/adaptation of the underlying facts rather than reproduction of GSI's own document.
