# Asset Schema

The manifest is the source of truth for the lifecycle and enables deterministic rebuilds. The starter JSON Schema is at [`spec/asset-manifest.schema.json`](../spec/asset-manifest.schema.json); it is intentionally small enough to evolve after the first fixture.

## Asset lifecycle

`briefed → generated → selected → normalized → validated → compiled → accepted`

`rejected` may follow `generated`, `selected`, `normalized`, or `validated`. A validator failure must not transition automatically to `accepted`.

## Required fields

| Field | Meaning |
| --- | --- |
| `id` | stable lowercase ID used by game data |
| `kind` | `sprite`, `tile`, `tileset`, `effect`, or `ui` |
| `source` | original inputs and license/provenance notes |
| `target` | dimensions, GBA mode, palette and tile contract |
| `generation` | optional provider/model/workflow/request metadata |
| `files` | native/preview/output paths; no overwriting candidates |
| `validation` | immutable results or a report reference |
| `animation` | explicit frames and named sequences when applicable |

## Example use

The forest-spirit example intentionally points at placeholder paths and is not an asset. It demonstrates a 32×32 4bpp sprite with a four-frame walk sequence. See [`examples/forest-spirit/theme.json`](../examples/forest-spirit/theme.json).

## Style contract fields

Keep subjective intent in a human-readable brief adjacent to the machine fields:

- silhouette and focal points;
- viewpoint and scale;
- palette role names rather than only hex codes;
- prohibited traits (anti-aliasing, text, gradients, stray pixels);
- animation intent and frame count range.

This makes a candidate selection reviewable without pretending that a prompt alone is a deterministic specification.
