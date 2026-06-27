# Example: JS/TS stack (AFK coding)

Concrete fill of 5 [SKILL.md](./SKILL.md) steps for TS project. Feedback loop let AI verify own work — critical for AFK/autonomous runs (e.g. Ralph Wiggum): AI hit RED, retry, no frustration.

## 1. Static check — TypeScript

TS = free feedback. Catch error AI never find without browser test. Use over JS.

```json
{ "scripts": { "typecheck": "tsc" } }
```

## 2. Tests — Vitest

Catch logic error. Basic unit test on core path keep AI on track.

```json
{ "scripts": { "test": "vitest" } }
```

## 3. Pre-commit gate — Husky

```sh
pnpm install --save-dev husky
pnpm exec husky init
```

`.husky/pre-commit` run all check:

```sh
npx lint-staged
npm run typecheck
npm run test
```

Any step fail → commit blocked, AI get error message.

Bonus loop: give LLM access to running local dev server, check frontend.

## 4. Formatter — lint-staged + Prettier

Auto-format staged file before commit.

```sh
pnpm install --save-dev lint-staged
```

`.lintstagedrc`:

```json
{ "*": "prettier --ignore-unknown --write" }
```

Run Prettier on staged file, auto-restage. All AI code match style now. Add ESLint here too — work nice with lint-staged.

## Why work for AI

Agent no frustrated by repeat. Code fail typecheck or test → agent retry. Make feedback loop (pre-commit especially) powerful for AI-driven dev.