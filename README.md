# people
Human roles, operators, and identities for the BlackRoad system.

## Overview

All `@mention` requests are routed exclusively to the local [Ollama](https://ollama.com) instance. No external AI providers (ChatGPT, GitHub Copilot, Claude, etc.) are used.

## Routing

See [`routing.yaml`](routing.yaml) for the full routing configuration.

| Mention | Backend | Notes |
|---|---|---|
| `@ollama` | Ollama (local) | Local AI service |
| `@copilot` | Ollama (local) | Routed to local Ollama, not GitHub Copilot |
| `@lucidia` | Ollama (local) | Routed to local Ollama |
| `@blackboxprogramming` | Ollama (local) | Operator identity, routed to local Ollama |

## Identities

Identity files live in the [`people/`](people/) directory. Each file is a YAML document describing the identity and its backend configuration.

- [`people/ollama.yaml`](people/ollama.yaml)
- [`people/copilot.yaml`](people/copilot.yaml)
- [`people/lucidia.yaml`](people/lucidia.yaml)
- [`people/blackboxprogramming.yaml`](people/blackboxprogramming.yaml)

## Principles

- **Local only** — all inference runs on the operator's private hardware
- **No telemetry** — no data is sent to third-party services
- **No vendor lock-in** — no dependency on any external AI provider
- **Offline capable** — works without internet access
