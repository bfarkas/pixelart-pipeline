# Tool and Provider Evaluation

This is a research-backed candidate list, not a tested-integration catalogue. MCP/API availability, licensing, prices, rate limits, and local model requirements must be rechecked at pilot time.

| Candidate | Role | Local/offline path | Evidence level | Pilot gate |
| --- | --- | --- | --- | --- |
| ComfyUI + pixel-art LoRA | local candidate generation | yes, planned on RTX 4060 Ti | planned architecture; no repository integration | produce ten 32×32 candidates with recorded latency/VRAM |
| ComfyUI PixelArt Detector | grid/palette cleanup | local | research link only | normalise a known fixture without blur or colour overflow |
| Flux Kontext dev/GGUF | variations and directed frame edits | local path proposed; 8 GB feasibility unverified | unverified | measure first-image, repeat-image, and VRAM use |
| PixelLab/MCP adapters | hosted pixel generation/possibly animation | no local fallback assumed | third-party MCP references only | confirm official API terms; compare fixed prompt set |
| Retro Diffusion | dedicated pixel workflow / optional animation | local Aseprite extension reported; animation cloud claim unverified | vendor/community links, no integration | compare one walk cycle for quality, cost, and provenance |
| Adobe Firefly | concepts/mood boards | hosted | vendor page only | use only for broad direction, never direct GBA export |
| Draw Things + LM Studio plugin | workstation experimentation | local on Mac proposed | linked integration concept only | verify supported model/workflow and repeatability |

## Evaluation protocol

Use the same three briefs: one 32×32 creature, one 16×16 tile, one 4-frame effect. For each provider collect:

- request input and exact workflow/model version;
- time, cost, queue/API errors, and local VRAM/RAM if relevant;
- candidate count and operator selection rate;
- validator failure categories; and
- one short provenance/licensing note.

Score 1–5 for pixel-grid fidelity, style consistency, silhouette readability, animation drift, repeatability, operating cost, and local fallback quality. Never use a marketing claim as a score.

## Integration policy

An adapter is only marked **implemented** after it has: a versioned request template, environment/config documentation, a recorded success fixture, structured error handling, and no secrets committed to the repository.
