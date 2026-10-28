# Pixel Art Pipeline

An implementation-ready specification for a low-touch pipeline that turns sketches, colour references, and photographs into reviewable pixel-art assets for a Game Boy Advance (GBA) and desktop game.

> **Status: specification only.** This repository contains no installed models, running MCP server, generated asset, benchmark, or tested provider integration. Statements tagged **Planned**, **Candidate**, or **Unverified** must not be read as completed work.

## Product intent

The operator selects the best candidate. Agents perform generation, deterministic cleanup, packaging, and checks. The primary target is GBA/retro-handheld art; a native desktop build can reuse the same native-resolution PNG sources. The first animation targets are platformer characters and effects.

The pipeline is deliberately hybrid:

- local ComfyUI generation and deterministic tooling are the privacy/offline fallback;
- hosted providers are optional comparison or animation accelerators;
- human review is a quality gate, not a pixel-editing workflow.

## What is in this repository

| Area | Purpose |
| --- | --- |
| [Architecture](docs/architecture.md) | Components, boundaries, and data flow |
| [Decisions](docs/decisions.md) | Confirmed choices and decision records |
| [Tool/provider evaluation](docs/tool-provider-evaluation.md) | Candidates, evidence level, and pilot criteria |
| [GBA constraints](docs/gba-constraints.md) | Hard packaging targets and validation rules |
| [Asset schema](docs/asset-schema.md) | Asset contract and starter JSON Schema |
| [Style examples](docs/style-examples.md) | Prompt and acceptance examples |
| [Validation and animation](docs/validation-and-animation.md) | Candidate selection, cleanup, and sprite workflows |
| [Implementation roadmap](docs/implementation-roadmap.md) | Staged delivery plan |
| [Research links](docs/research.md) | Source material and evidence caveats |
| [Assumptions](docs/assumptions.md) | Open, unverified inputs |
| [Starter schema](spec/asset-manifest.schema.json) | Machine-readable manifest contract |
| [Example theme](examples/forest-spirit/theme.json) | Small, non-production manifest example |

## Intended end-to-end flow

`brief + reference → generate candidates → operator selects → grid/palette cleanup → validate → compile/package → preview in game/emulator`

All state transitions should be recorded in an asset manifest. Raw references and model/provider metadata are retained for provenance; distributable output is only promoted after validation.

## Design rules

1. Native resolution first. Never use AI upscaling to make pixel art.
2. Treat generated images as candidates, never as GBA-ready exports.
3. Enforce palette, grid, dimensions, tile, and animation contracts deterministically.
4. Keep generation adapters separate from schemas, compiler, and validators.
5. Preserve original references and provenance; do not publish protected-IP-derived assets.
6. A failed validator must block promotion rather than silently adjusting production output.

## Start here

1. Read the [architecture](docs/architecture.md) and [assumptions](docs/assumptions.md).
2. Choose a pilot provider from the [evaluation matrix](docs/tool-provider-evaluation.md).
3. Implement Stage 0–2 of the [roadmap](docs/implementation-roadmap.md) before connecting paid or cloud services.
4. Use the [asset schema](docs/asset-schema.md) as the contract for the first 32×32 creature pilot.

## Scope and non-goals

This repository specifies an asset pipeline, not the game engine, a model-training system, or a promise that any provider produces export-ready art. Theme-specific LoRA training and paid animation are deliberately deferred until a measured pilot demonstrates value.

## License and IP note

Do not place unlicensed reference art or protected characters in distributable asset sets. A private experiment may have different risk tolerance, but any shareable theme should use original characters, names, and visual motifs.
