# Validation and Animation Workflow

## Candidate to accepted asset

1. Create a brief with target dimensions, palette role intent, asset kind, and source provenance.
2. Generate one or more candidates through an adapter; write immutable candidate metadata.
3. Present nearest-neighbour 1×/4× views and a simple in-context preview.
4. Record the operator's selected candidate ID and reason.
5. Detect/confirm pixel grid, resize to target only with nearest-neighbour, and quantise to the declared palette contract.
6. Run static validation. A failure yields a report and a `rejected` or `needs-rework` result; it does not self-promote.
7. For animated assets, validate frames and sequences before compilation.
8. Compile/package a passing derivative, then inspect it in desktop runtime and emulator.

## Animation contract

Represent animation explicitly rather than relying on filenames:

```json
{
  "sequence": "walk",
  "loop": true,
  "frames": ["walk_00", "walk_01", "walk_02", "walk_03"],
  "frameDurationMs": 100,
  "anchor": {"x": 16, "y": 31}
}
```

Initial checks should include:

- every frame matches declared dimensions, palette policy, and anchor;
- frame order is complete and duration is present;
- opaque bounding-box and centre displacement stay under declared tolerance (warn, not necessarily fail);
- feet/contact pixels align with baseline during locomotion (warn/fail based on brief);
- no frame introduces an undeclared palette bank;
- sprite sheets have no accidental gutters or frame-boundary overlap.

## Generation strategy for platformer animation

Start from an approved idle/key pose. Use an image-edit or provider animation candidate flow to create individual frames, then normalize every frame against the original style contract. This prioritises consistency and makes drift visible. Dedicated animation services remain optional until a fixed-prompt pilot proves their advantage.

## Effects

Effects may tolerate more shape variation than character walk cycles, but they still need a declared frame count, loop policy, anchor, palette, and native dimensions. Validate them as a named sequence; do not accept a GIF/video as the production source of truth.
