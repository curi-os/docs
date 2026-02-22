CuriOS
A Conversational OS where the primary interface is a chat. Instead of clicking through menus, users type what they want (“set up my provider”, “show my settings”, “change my name”), and the server routes the message through a set of conversational flows to produce the next response.

This repo focuses on making chat interactions reliable and stateful: each message is handled in the context of a session (who the user is, which step they’re on, what’s configured), so the system can guide the user through onboarding and “OS-like” actions.

What is a “Conversational OS”?
A Conversational OS is an interface pattern where:

Chat is the UI: commands, settings, onboarding, and “apps” are invoked through natural language.
State is explicit: the system remembers where you are in a flow (e.g., signing in, setting a provider, updating a password).
The backend does the orchestration: it turns free-form text into deterministic actions via:
simple rule-based commands for common actions, and/or
an LLM-powered intent classifier for flexible phrasing
In practice, CuriOS behaves like a small operating layer that lives inside a chat thread.

How it works (high level)
Client sends a message to the server (e.g., POST /chat).
The server resolves the session (session id, user identity if authenticated, existing conversation state).
The message is routed through a state machine:
If the user is not authenticated → auth/onboarding flow
If an AI provider isn’t configured → provider setup flow
Otherwise → “ready” state, where commands/intents are handled
The server returns the next assistant message and persists:
updated conversation context/state
message history (optionally redacting/encrypting secrets)
Core capabilities
Session-based conversations (chat context persists across turns)
Onboarding flows (auth + provider configuration)
Provider abstraction (swap between LLM backends/providers)
Intent handling (map user messages to a small set of system intents/actions)
Message history (store/retrieve conversation messages; redact secrets when needed)
API (typical)
Your exact routes may differ, but a typical setup includes:

POST /chat — send a user message, receive assistant reply
GET /session — fetch current session context/state
GET /messages — fetch message history (often cursor-based)
DELETE /session — clear/reset a session
GET /health — health check
Getting started
Prerequisites
Node.js (LTS recommended)
npm (or pnpm/yarn)
A database/auth provider if your deployment persists users/sessions (commonly Supabase/Postgres)
Install
Configure environment
Create a .env (or copy from .env.example if present).

Common environment variables you may need:

PORT
BASE_URL (if used by your deployment)
Database/auth (e.g., Supabase URL/keys)
Provider secrets (if you store encrypted API keys)
PROVIDER_KEY_ENCRYPTION_SECRET (recommended if encrypting secrets at rest)
Example template:

Run in dev
Type-check / build (if available)
Project concepts (mental model)
1) State machine over “free chat”
Even when a user types natural language, the system operates in explicit states (e.g., “auth”, “provider setup”, “ready”). This prevents the experience from becoming ambiguous and makes multi-step tasks dependable.

2) Deterministic commands + LLM intent classification
For common actions (“help”, “change provider”, “show settings”), deterministic handling reduces confusion. For flexible phrasing, an intent classifier can map text into a controlled set of intents.

3) Provider abstraction
The server can support multiple LLM backends (e.g., local, OpenAI-compatible, custom HTTP) behind a single interface. This keeps the “OS” logic independent from any one model vendor.

4) Security & privacy by design
Treat API keys/passwords as secrets (encrypt at rest where possible)
Redact secrets in message history responses
Validate inputs (email/password/name/etc.)
Enforce access control policies for user/session data
“Docs” user experience
When a user clicks Docs, they should learn:

What CuriOS is (a Conversational OS)
What the server does (routing + state + persistence + providers)
How to run it (env + dev command)
What the main flows are (auth → provider → ready)
Where to configure providers and persistence (env + database/auth)
This README is designed to serve as that landing page.

Roadmap ideas (optional)
More “apps” (notes, files, browser automation) behind conversational intents
Tool/plugin system (structured tool calls with safety checks)
Fine-grained permissions (per intent/app)
Better session replay/debugging tools
License
Add your license here (e.g., MIT / Apache-2.0 / proprietary).
