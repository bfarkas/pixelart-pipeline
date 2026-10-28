# Style Examples and Acceptance Briefs

These examples are briefs, not ready-to-run prompts or demonstrated model outputs. They support candidate generation and review while protecting the GBA contract from aesthetic drift.

## Example: forest-spirit platformer creature

| Item | Brief |
| --- | --- |
| Target | 32×32 sprite, side view, 4bpp, one palette bank |
| Silhouette | round mossy body, two leaf ears, short feet; readable at 1× |
| Palette roles | transparent, outline, deep shadow, body mid, body light, leaf dark, leaf light, accent |
| Animation | idle: 2–3 frames; walk: 4–6 frames; no camera motion |
| Avoid | anti-aliasing, airbrushed gradients, text, blurry resampling, scene background |
| Acceptance | strong 1× silhouette, ≤15 opaque colours after normalization, feet stay on baseline during walk |

Illustrative candidate prompt:

> Original forest-spirit platformer character, 32 by 32 pixel sprite, side view, rounded moss body with leaf ears, limited retro handheld palette, hard-edged pixels, clean dark outline, transparent background, walking-game silhouette; no text, no smooth gradients, no anti-aliasing.

The provider may return an arbitrary image size. The normalizer must create the 32×32 derivative and record the transform; it must not silently crop meaningful anatomy.

## Example: background tile

| Item | Brief |
| --- | --- |
| Target | 16×16 or 32×32 source composed of 8×8 tiles |
| Intent | looping mossy stone ground with readable walkable top edge |
| Acceptance | seamless at all edges, palette bank declared, dedup report available |
| Avoid | one-off painted lighting that breaks repetition, subpixel texture, accidental seams |

## Review at three scales

1. **1×:** silhouette, stray pixels, palette readability.
2. **Nearest-neighbour 4×:** anatomy, cluster quality, animation frame drift.
3. **In-context:** collision edge, repeated tiles, parallax/background separation.

The operator selects a candidate; the subsequent tooling should produce these views and validation reports automatically.
