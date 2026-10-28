# Architecture

## Status legend

- **Specified**: contract designed in this repository.
- **Planned**: intended implementation, not present here.
- **Candidate**: a possible external/local provider; not integrated or endorsed.
- **Unverified**: inherited research claim or operating assumption awaiting a pilot.

## Component model

```text
references + asset brief
        │
        ▼
generation adapter ──► candidate PNGs + provenance
        │                       │
        │ operator selects      ▼
        └────────────────► deterministic normalizer
                                  │
                                  ▼
                         asset manifest + native PNG
                                  │
                    ┌─────────────┴─────────────┐
                    ▼                           ▼
             static validator             animation validator
                    │                           │
                    └─────────────┬─────────────┘
                                  ▼
                          GBA compiler/exporter
                                  │
                        tiles / palettes / preview
```

## Responsibilities and boundaries

| Component | Status | Owns | Must not own |
| --- | --- | --- | --- |
| Brief and reference store | Specified | intent, source licence/status, target dimensions | derived exports |
| Generation adapter | Planned | provider-specific request/response translation, request IDs | palette policy or compiler rules |
| Candidate store | Planned | immutable generated candidates and provenance | promotion decision |
| Selection gate | Planned | operator's chosen candidate ID and review notes | pixel manipulation |
| Normalizer | Planned | grid detection, native downscale, quantisation, nearest-neighbour preview | creative generation |
| Validator | Planned | contract checks and machine-readable reports | automatic acceptance of failures |
| GBA compiler | Planned | tile slicing, deduplication, palette-bank allocation and engine export | provider calls |
| Runtime preview | Planned | visual inspection on desktop/emulator | source mutation |

## Local-first deployment shape

The proposed local fallback is ComfyUI on the Windows RTX 4060 Ti machine, accessed through its HTTP API from a small client. Keep it LAN-only; if it has no authentication, restrict firewall access to the trusted local subnet. The Mac workstation can drive requests and handle review. The 6 GB homelab GPU is not assumed capable of the proposed generation workloads.

The repository should eventually contain `tools/art-pipeline/`:

```text
tools/art-pipeline/
  adapters/          # provider implementations, no compiler policy
  workflows/         # versioned provider workflow templates
  pipeline/          # normalizer, manifest handling, provenance
  validators/        # independent static/animation checks
  compiler/          # GBA-oriented export
  tests/             # fixture-driven contract tests
```

No such code is implemented yet.

## Data contracts

1. A request creates an immutable candidate record with provider/model/workflow identifiers.
2. Selection records an accepted candidate but does not overwrite it.
3. Normalisation produces a new derivative at native resolution plus palette metadata.
4. Validation consumes the derivative and manifest, returning pass/fail findings.
5. Compilation is allowed only for a passing validation report and writes a separate build artifact.

This separation allows local and cloud adapters to be swapped without changing the game-facing asset contract.
