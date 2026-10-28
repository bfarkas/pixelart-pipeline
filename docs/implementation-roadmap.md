# Staged Implementation Roadmap

Each stage has a demonstrable exit criterion. Nothing below is implemented by this documentation commit.

## Stage 0 — Contracts and fixtures

- Add a JSON Schema validator and a hand-authored fixture manifest.
- Add a small original 32×32 creature, one 16×16 tile, and one four-frame effect as fixtures (or placeholders that clearly cannot be built).
- Define accepted/rejected manifest states and report format.

**Exit:** CI validates the fixture manifest and intentionally broken fixtures fail with stable codes.

## Stage 1 — Deterministic normalizer and static validator

- Implement image load, nearest-neighbour scaling, RGB555 conversion, indexed palette audit, alpha policy, and tile alignment checks.
- Produce a validation JSON report and nearest-neighbour preview.

**Exit:** fixture passes; anti-aliased, over-palette, and non-aligned fixtures fail predictably.

## Stage 2 — GBA-oriented compiler prototype

- Slice 8×8 tiles, deduplicate tiles and flips, allocate declared palette banks, and emit a documented intermediate format.
- Add tile/bank budget errors and metadata outputs.

**Exit:** a fixture compiles; output is inspected against the chosen real GBA toolchain and emulator. Compatibility remains unclaimed before this point.

## Stage 3 — Local generation adapter

- Version ComfyUI workflow templates outside the ComfyUI install.
- Add configuration via environment variables/config file, without secrets in Git.
- Record workflow/model versions, request IDs, duration, and errors in candidate metadata.

**Exit:** one original pilot brief creates candidates, the operator selects one, and the normalizer/validator process it end to end.

## Stage 4 — Animation workflow

- Add frame-sequence manifest handling, contact-sheet/preview generation, anchor checks, and walk/effect fixtures.
- Measure character consistency and validator failure rate for image-edit frames.

**Exit:** an original 4–6 frame walk cycle and 4-frame effect reach in-context preview with reports.

## Stage 5 — Provider pilots and optional adapters

- Run the identical three-brief evaluation for PixelLab and Retro Diffusion only after terms, pricing, and provenance are confirmed.
- Keep local output as the fallback and write a concise pilot report.

**Exit:** adopt/reject each provider with measured evidence, not a marketing comparison.

## Stage 6 — Theme pack and integration hardening

- Build a first original theme manifest; add asset inventory, visual regression/contact sheets, and emulator smoke test.
- Reconsider theme LoRA training only with a reviewed, rights-cleared dataset.

**Exit:** repeatable build of a complete small theme with an auditable provenance record.
