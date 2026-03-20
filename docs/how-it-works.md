---
layout: default
title: How It Works
nav_order: 2
---

# How It Works

## High-level flow

1. **You send a message** (e.g., "help", "sign in", "change provider").
2. CuriOS **resolves your session context** (who you are, where you are in the flow, what's configured).
3. Your message is routed through a **state machine**:
   - If you're not authenticated → auth/onboarding flow
   - If an AI provider isn't configured → provider setup flow
   - Otherwise → "ready" state, where commands/intents are handled
4. CuriOS returns the next reply and **persists**:
   - updated conversation context/state
   - message history (optionally redacting/encrypting secrets)

---

## State machine over "free chat"

Even when you type natural language, the system operates in explicit **states** (e.g., "auth", "provider setup", "ready"). This prevents the experience from becoming ambiguous and makes multi-step tasks dependable.

## Deterministic commands + intent classification

For common actions ("help", "change provider", "show settings"), deterministic handling reduces confusion. For flexible phrasing, an intent classifier can map text into a controlled set of intents.
