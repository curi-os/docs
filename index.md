---
layout: home
title: Home
nav_order: 1
---

# CuriOS

**CuriOS** is a *Conversational OS*: the primary interface is a chat. Instead of clicking through menus, users type what they want ("set up my provider", "show my settings", "change my name"), and CuriOS routes the message through conversational flows to produce the next response.

The core idea is making chat interactions **reliable** and **stateful**: each message is handled in the context of a session (who the user is, which step they're on, what's configured), so CuriOS can guide users through onboarding and "OS-like" actions.

---

## What is a "Conversational OS"?

A Conversational OS is an interface pattern where:

- **Chat is the UI**: commands, settings, onboarding, and "apps" are invoked through natural language.
- **State is explicit**: the system remembers where you are in a flow (e.g., signing in, setting a provider, updating a password).
- **The system does the orchestration**: it turns free-form text into deterministic actions via:
  - simple rule-based commands for common actions, and/or
  - an LLM-powered intent classifier for flexible phrasing

In practice, CuriOS behaves like a small operating layer that lives inside a chat thread.

---

## Common things you can say

- **Help**: "help"
- **Settings**: "show my settings"
- **Profile**: "change my name"
- **Security**: "change my password"
- **Providers**: "change provider"
- **Account**: "delete my user"
