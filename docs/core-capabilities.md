---
layout: default
title: Core Capabilities
nav_order: 3
---

# Core Capabilities

CuriOS provides the following core capabilities:

- **Session-based conversations** — context persists across turns
- **Onboarding flows** — auth + provider configuration
- **Provider abstraction** — swap between LLM backends/providers
- **Intent handling** — map user messages to a small set of system intents/actions
- **Message history** — store/retrieve conversation messages; redact secrets when needed

---

## Provider Abstraction

CuriOS can support multiple LLM backends (e.g., local, OpenAI-compatible, custom HTTP) behind a single interface. This keeps the "OS" logic independent from any one model vendor.

---

## Security & Privacy by Design

- Treat API keys/passwords as secrets (encrypt at rest where possible)
- Redact secrets in message history responses
- Validate inputs (email/password/name/etc.)
- Enforce access control policies for user/session data
