# Decisions

## Confirmed product decisions

| Decision | Rationale | Consequence |
| --- | --- | --- |
| Operator selects candidates; agents perform edits | Low-touch production is the stated preference | Review UI/report is mandatory; manual pixel editing is an exception |
| Prioritise GBA and retro handheld | The intended target is a GBA remake plus desktop build | Native art and validator rules target GBA constraints |
| Use a hybrid service model | Local fallback is required, but online tools may accelerate work | Every provider needs an adapter and a no-provider fallback |
| Prioritise platformer sprites/effects | First animation need | Validate named frame sequences and silhouettes before complex rigs |
| Treat themes as data | The game is intended to be theme-agnostic | Theme manifests own palettes, asset IDs, and source/provenance |

## Architecture decisions

### ADR-001: Generated pixel images are candidates, not exports

**Decision:** Normalise and validate every selected output before packaging.

**Why:** Research states no generator should be assumed to produce GBA-ready art directly. Deterministic checks protect against anti-aliasing, wrong grids, incompatible palettes, and dimension drift.

### ADR-002: Preserve native-resolution source art

**Decision:** Store canonical PNGs at target resolution and only scale previews with nearest-neighbour sampling.

**Why:** It avoids blur, keeps desktop and GBA paths aligned, and makes tile/palette inspection reliable.

### ADR-003: Separate provider adapters from asset compiler policy

**Decision:** Adapters may create candidates; the compiler never calls providers.

**Why:** Cloud availability, licensing, cost, and MCP/API details change independently of the game contract.

### ADR-004: Defer theme LoRA training

**Decision:** Do not train a theme LoRA until hand-finished pilot assets and measured baselines exist.

**Why:** The reported feasibility/timing on 8 GB VRAM is unverified, and a style dataset needs a coherent quality bar.

### ADR-005: Cloud animation is an optional accelerator

**Decision:** First implement an image-edit/frame pipeline; evaluate a dedicated cloud animation API only as a pilot.

**Why:** Local animation availability, cost, and quality were not verified in the research.

## Decisions still required

- Select a game engine/export target and confirm its exact GBA asset format.
- Define legal provenance requirements for private versus shareable themes.
- Measure the actual ComfyUI model stack on the 8 GB GPU.
- Decide whether first release needs 4bpp only or any 8bpp exceptions.
