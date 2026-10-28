# Assumptions and Unknowns

## Unverified assumptions carried from research

| Assumption | Why it matters | Required verification |
| --- | --- | --- |
| The Windows RTX 4060 Ti has 8 GB VRAM | determines feasible local models | inspect hardware and record driver/RAM |
| Flux Kontext dev/GGUF can operate acceptably on 8 GB VRAM | local variation workflow depends on it | benchmark fixed images, VRAM, RAM, and latency |
| SDXL LoRA training is feasible on that GPU in roughly an hour | style-consistency plan | train a tiny rights-cleared pilot and log settings/results |
| Retro Diffusion local extension works locally but animation requires cloud | affects cost/fallback | verify official terms and product capability |
| PixelLab has usable MCP/API support | affects agent-driven requirement | verify official interface, authentication, and licence |
| ComfyUI is safe to expose on LAN-only | affects system security | firewall test; do not expose it publicly unauthenticated |
| grit/devkitPro target details match this compiler contract | affects shipped format | round-trip fixture in actual target/toolchain/emulator |

## Required product choices

- Exact game runtime/engine and its accepted asset layouts.
- Whether palette/tile policy has 4bpp-only exceptions.
- The destination/retention policy for photos and cloud-provider inputs.
- Rights and attribution policy for source references and generated outputs.
- The acceptable operator review time per asset batch.

## Known limitations

Generation may resemble pixel art without being grid-true. Automated cleanup can enforce technical bounds, but it cannot guarantee appealing clusters, pose readability, character consistency, or legal clearance. The operator therefore remains the selection gate.
