# Dossier Format

Status: v1 — 2026-09-05

This document defines the **dossier** — kataribe's own primary artifact. See
`CLAUDE.md` for what a dossier is and why it exists; this document is just the
concrete schema.

A dossier is **kataribe's unique work, not shared with any sibling repo.**
`dwg7/ferspas57` has no equivalent concept — their narratives are authored
directly from verified source-data checks, with no separate richer document
behind them (`DECISIONS.md` D2). A dossier is deliberately richer than
anything a Cartographer link can carry: verified facts, their sources, per-layer
audience notes, and — importantly — honest caveats about what map data can and
cannot show for a given layer (see the `map_caveat` field below, motivated
directly by a real finding in the first dossier).

## What belongs in a dossier vs. what gets looked up at generation time

**A dossier contains only what a fixed primary source already establishes** —
GSI's own explanatory document, a Library's actual checked data (e.g.
kitavolca's real VLCM tile contents), a design proposal's already-settled
framing. It does not contain present-day specifics that could change year to
year or that nobody has actually looked up yet (current crop types, whether a
memorial exists, this year's anniversary events, etc.).

**Anything else is deliberately left for narrative.json generation time** —
when a real asker's question triggers Staff to actually build the
Cartographer-facing projection, that is also the moment for Staff to do real,
citable research into whatever current/supplementary facts the chosen layer
needs, rather than freezing a guess into the versioned dossier ahead of time
(hfu, 2026-09-05). This is not a loophole in the anti-fabrication rule — it's
the opposite of fabrication: a live, verifiable lookup against a real source,
done at the moment it's needed, is more honest than a stale or invented detail
baked into a document that isn't re-checked on every use. What the
anti-fabrication rule still forbids, at either stage, is asserting something
with no real source behind it.

Practically: a layer whose *structural* claim is already dossier-worthy (e.g.
"this deposit area is farmland today" — a slow-changing, already-verified fact)
can go in `facts` now. A layer whose value depends on specifics nobody has
gathered yet stays `status: incomplete` in the dossier and gets its concrete
content filled in live, at generation time, sourced then.

## Relationship to narrative.json / Cartographer links

A dossier is **not** a narrative.json and is not written against either
`ferspas57`'s or `spiccato`'s schema. Each dossier layer carries a
`map_projection_hint` — enough information (required layer IDs, center, zoom)
to mechanically build a Cartographer-facing artifact (a `ferspas57`-style
narrative step, or a `spiccato` `#q=` link) — but that artifact is a disposable,
regenerable *projection* of the dossier, not the dossier itself (`DECISIONS.md`
D2). This is what lets the dossier be written before the Cartographer choice is
settled.

## Schema

```json
{
  "dossier_version": "kataribe-dossier/v1",
  "event": {
    "name_ja": "...",
    "name_en": "...",
    "date": "YYYY-MM-DD",
    "place_ja": "..."
  },
  "sources": [
    {
      "id": "short-slug",
      "citation": "full citation, including URL if online",
      "usage_basis": "copyright/usage-rights note — required for any non-CC0 source",
      "gathered": "YYYY-MM-DD"
    }
  ],
  "layers": [
    {
      "layer_id": "hazard | livelihood | place-identity | ...",
      "title_ja": "...",
      "audience_examples": ["who this layer is typically for"],
      "facts": [
        { "text": "one verified claim, in plain prose", "source": "source id from `sources` above" }
      ],
      "map_caveat": "optional: an honest note about what the associated map data does/doesn't show — do not omit this if the map would otherwise visually overclaim",
      "map_projection_hint": {
        "required_layers": ["source_id, from whichever Cartographer catalog is targeted"],
        "center": [lng, lat],
        "zoom": 0,
        "note": "optional guidance for whoever builds the actual link"
      },
      "status": "optional: 'incomplete' + what's missing, when a layer isn't yet fact-complete enough to hand to a real asker"
    }
  ]
}
```

## Rules

- **Every fact traces to a `sources` entry.** No fact without a `source` id. An
  entry with no real source behind it yet must not be written as if verified —
  mark the layer's `status` as `incomplete` instead (same anti-fabrication
  discipline as `ferspas57`'s `NARRATIVES.md`).
- **`map_caveat` is not optional when it matters.** If the best available map
  layer for a dossier layer covers less ground than the facts describe (as
  happened with the first dossier's hazard layer — see `HANDOVER.md`), say so
  explicitly here. A Staff must never let a map imply more than the underlying
  data shows.
- **`map_projection_hint` names layer IDs from a real, checked catalog** —
  never a plausible-sounding but unverified `source_id`. If nothing in the
  catalog actually matches, say so in `map_caveat` / `status` rather than
  inventing one (this is exactly what happened when `spiccato`'s session
  checked for a mudflow-specific layer and found only the general
  `vlcd_tokachi` VLCM layer — see `HANDOVER.md`).
- **`status: incomplete` is a valid, expected state**, not a failure — a layer
  should carry it rather than be filled with plausible-sounding but ungathered
  specifics.
