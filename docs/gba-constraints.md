# GBA Constraints and Compiler Contract

This document defines the initial *target contract*, not evidence of a finished compiler. Integrate against the actual engine/toolchain only after a fixture export succeeds in an emulator.

## Initial target rules

| Concern | Initial rule | Validation result |
| --- | --- | --- |
| Colour representation | RGB555 | fail if export cannot map colour deterministically |
| 4bpp palette | 16 entries per palette, including transparent index 0 | fail when an assigned asset needs more than 15 opaque colours |
| Palette banks | up to 16 sprite and 16 background banks | fail on budget overflow |
| Tile size | 8×8 pixels | fail when dimensions are not tile-aligned for tile assets |
| Background reuse | deduplicate identical tiles and horizontal/vertical flips | report savings and mapping |
| Sprites | dimensions/modes must be explicitly declared by the engine target | fail on absent or unsupported declaration |
| Canonical source | native-resolution indexed/quantised PNG derivative | fail on unresolved grid or alpha policy |

The 4bpp policy above expresses the original research intent: 15 visible colours plus transparent palette index 0. Verify transparency and palette-bank details against the chosen runtime before declaring compatibility.

## Required static validation

For every promoted asset, the validator should emit JSON with stable finding IDs:

1. `dimensions`: positive dimensions and declared target compatibility.
2. `grid`: pixel grid/no unintended smoothing; target tile alignment where required.
3. `palette`: opaque colour count, palette ID, RGB555 conversion report.
4. `alpha`: only the declared transparent index/policy is used.
5. `tile-budget`: tiles before/after deduplication and flip reuse.
6. `bank-budget`: palette allocation and total use.
7. `manifest`: source, derivative, and provenance records exist.

## Compiler outputs (planned)

```text
build/<theme>/<asset>/
  asset.tiles.bin
  asset.palette.bin
  asset.tilemap.bin          # backgrounds only
  asset.meta.json            # hashes, dimensions, palette/tile mapping
  asset.preview.png          # nearest-neighbour inspection render
  validation-report.json
```

Do not claim `grit` compatibility until an actual generated artifact has been compared with a real toolchain output and loaded successfully.
