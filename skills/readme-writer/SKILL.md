---
name: readme-writer
description: Write a README that sells the project. Treat it like a landing page. Use when the user asks to write, create, or improve a README.
argument-hint: (library, app, portfolio)
disable-model-invocation: true
---

Tania Rascia rule: if someone can't understand AND run your project in 5 minutes from the README, you failed.

The README is the landing page. First thing recruiters, collaborators, and users see.

## Required structure

1. **Title + one-line hook** — sells the project. Not "This is a project for...". Use "Auth that works. No pain."
2. **Badges** (npm/downloads/license) if published.
3. **Why / features** — 3 bullets, benefit-first with emoji: `⚡ **30s to start** - ...`
4. **Install** — one copy-pasteable line in a `bash` block. No "first make sure you have Node 18+".
5. **Quick usage** — real code that runs when copy-pasted. Never pseudocode.
6. **Screenshot/GIF** if there's a UI: `![Demo](./demo.gif)`
7. **Examples / Docs** links if they exist.
8. **License** — one line.

Drop sections the project doesn't need. Minimum viable README (title + install + usage + license) beats nothing.

## By type ($ARGUMENTS)

- `library` — full structure above. Hook, badges, install, usage, examples, docs.
- `app` — live demo link first, then features, install.
- `portfolio` — demo link, tech stack, "What I learned" bullets. Skip install if not runnable.

## Rules

- First line vends. Cut "This is a...".
- Every code block must actually run.
- Show, don't tell. GIF over paragraph for UI.
- Match the project's language (read package.json / source first).
