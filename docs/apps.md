---
layout: default
title: Apps
nav_order: 4
---

# Apps

CuriOS supports switching into different **app contexts** from within the chat thread — like an OS, but conversational. Each app exposes its own set of intents and commands, all accessible through natural language.

---

## Available Apps

| App | Status | Description |
|-----|--------|-------------|
| **System** | ✅ Available | Manage config and user settings through guided chat flows |
| **Browser** | ✅ Available | Navigate the web in a conversational way — ask, click, and summarize |
| **Files** | 🔜 Coming soon | Manage files and folders from chat |
| **Notes** | 🔜 Coming soon | Save and organize notes inside your sessions |

---

## Browser App

The **Browser app** lets you navigate the web conversationally without leaving the chat thread. Once you switch into the Browser context, you can open sites, interact with pages, extract information, and automate tasks — all by describing what you want in plain language.

### Entering the Browser App

To enter the Browser app, type:

```
"use Browser"
```

To return to the main System context, type:

```
"exit"
```

### What You Can Do

| Intent | Example message |
|--------|----------------|
| Enter Browser | `"use Browser"` |
| Open a site | `"open nytimes.com and give the latest news"` |
| Make actions | `"log in to my blog and publish and write a draft post about AI"` |
| Research | `"Find a job as Software developer on jobindex.com"` |
| Summarize a page | `"What you think about this page: https://curi-os.github.io/curi-os/"` |
| Extract info | `"Get the key info from this page"` |
| Navigate tabs | `"open a new tab and open Instagram"` |

### How It Works

1. **You describe the task** — e.g., `"open nytimes.com and give the latest news"`
2. **The Browser app navigates the web** — it opens the URL and interacts with the page on your behalf
3. **Results are returned in chat** — summaries, extracted data, or confirmation of completed actions come back as a chat message
4. **You stay in context** — you can ask follow-up questions or give new instructions without leaving the thread

The Browser app is part of the [curios-browser](https://github.com/curi-os/curios-browser) front-end, built with React and TypeScript, which provides the chat-first UI that drives the browser experience.

---

## System App

The **System app** is the default context when you open CuriOS. It handles user settings, authentication, and provider configuration through guided conversational flows.

| Intent | Example message |
|--------|----------------|
| Help | `"help"` |
| Settings | `"show my settings"` |
| Profile | `"change my name"` |
| Security | `"change my password"` |
| Providers | `"change provider"` |
| Account | `"delete my user"` |
| Switch app | `"use Browser"` |
