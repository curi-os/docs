# CuriOS

**CuriOS** is a *Conversational OS*: the primary interface is a chat. Instead of clicking through menus, users type what they want (“set up my provider”, “show my settings”, “change my name”), and CuriOS routes the message through conversational flows to produce the next response.

The core idea is making chat interactions **reliable** and **stateful**: each message is handled in the context of a session (who the user is, which step they’re on, what’s configured), so CuriOS can guide users through onboarding and “OS-like” actions.

---

## What is a “Conversational OS”?

A Conversational OS is an interface pattern where:

- **Chat is the UI**: commands, settings, onboarding, and “apps” are invoked through natural language.
- **State is explicit**: the system remembers where you are in a flow (e.g., signing in, setting a provider, updating a password).
- **The system does the orchestration**: it turns free-form text into deterministic actions via:
  - simple rule-based commands for common actions, and/or
  - an LLM-powered intent classifier for flexible phrasing

In practice, CuriOS behaves like a small operating layer that lives inside a chat thread.

---

## How it works (high level)

1. **You send a message** (e.g., “help”, “sign in”, “change provider”).
2. CuriOS **resolves your session context** (who you are, where you are in the flow, what’s configured).
3. Your message is routed through a **state machine**:
   - If you’re not authenticated → auth/onboarding flow
   - If an AI provider isn’t configured → provider setup flow
   - Otherwise → “ready” state, where commands/intents are handled
4. CuriOS returns the next reply and **persists**:
   - updated conversation context/state
   - message history (optionally redacting/encrypting secrets)

---

## Core capabilities

- **Session-based conversations** (context persists across turns)
- **Onboarding flows** (auth + provider configuration)
- **Provider abstraction** (swap between LLM backends/providers)
- **Intent handling** (map user messages to a small set of system intents/actions)
- **Message history** (store/retrieve conversation messages; redact secrets when needed)

---

## Common things you can say

- **Help**: “help”
- **Settings**: “show my settings”
- **Profile**: “change my name”
- **Security**: “change my password”
- **Providers**: “change provider”
- **Account**: “delete my user”

---

## Project concepts (mental model)

### 1) State machine over “free chat”

Even when you type natural language, the system operates in explicit **states** (e.g., “auth”, “provider setup”, “ready”). This prevents the experience from becoming ambiguous and makes multi-step tasks dependable.

### 2) Deterministic commands + intent classification

For common actions (“help”, “change provider”, “show settings”), deterministic handling reduces confusion. For flexible phrasing, an intent classifier can map text into a controlled set of intents.

### 3) Provider abstraction

CuriOS can support multiple LLM backends (e.g., local, OpenAI-compatible, custom HTTP) behind a single interface. This keeps the “OS” logic independent from any one model vendor.

### 4) Security & privacy by design

- Treat API keys/passwords as secrets (encrypt at rest where possible)
- Redact secrets in message history responses
- Validate inputs (email/password/name/etc.)
- Enforce access control policies for user/session data

---

## “Docs” user experience

When you click **Docs**, you should learn:

- What CuriOS is (a Conversational OS)
- How the experience is structured (auth → provider → ready)
- What you can do (settings, profile, providers, account actions)
- How CuriOS keeps conversations reliable (explicit state + intent routing)

---

## Roadmap ideas (optional)

- More “apps” (notes, files, browser automation) behind conversational intents
- Tool/plugin system (structured tool calls with safety checks)
- Fine-grained permissions (per intent/app)
- Better session replay/debugging tools
