# people
Human roles, operators, and identities for the BlackRoad system.

## People

| GitHub | Name | Role |
|--------|------|------|
| [@blackboxprogramming](https://github.com/blackboxprogramming) | Alexa Amundson | Operator, Founder |

## Overview

All `@mention` requests are routed exclusively to the local [Ollama](https://ollama.com) instance. No external AI providers (ChatGPT, GitHub Copilot, Claude, etc.) are used.

## Authentication (OAuth/OIDC)

Authentication is handled locally via a self-hosted OAuth 2.0 / OIDC provider. No external identity providers (Google, GitHub OAuth, Auth0, Okta, etc.) are used.

See [`auth.yaml`](auth.yaml) for the full authentication and network configuration, including Tailscale mesh and optional Cloudflare Tunnel settings.

- **Provider**: Self-hosted [Authentik](https://goauthentik.io) on `localhost:9000`
- **Network**: Private [Tailscale](https://tailscale.com) mesh — all traffic stays within the operator's infrastructure
- **External exposure**: Opt-in only via [Cloudflare Tunnel](https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/) — nothing is exposed by default
- **Authorized operators**: `@blackboxprogramming`, `@lucidia`
- **Blocked providers**: OpenAI, Anthropic, GitHub Copilot, Codex, Google, Auth0, Okta

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
- **User sovereignty** — the operator controls all infrastructure
