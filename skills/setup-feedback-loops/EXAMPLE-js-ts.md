# Example: JS/TS stack (AFK coding)

Concrete fill of 5 [SKILL.md](./SKILL.md) steps for TS project. Feedback loop let AI verify own work — critical for AFK/autonomous runs (e.g. Ralph Wiggum): AI hit RED, retry, no frustration.

## 1. Static check — TypeScript + oxlint

TS = free feedback. Catch error AI never find without browser test. Use over JS.

```json
{ "scripts": { "typecheck": "tsc" } }
```

oxc = Rust toolchain: `oxlint` (lint) + `oxfmt` (format). ~50x faster than ESLint/Prettier, zero config. Catch bug + bad pattern.

```sh
pnpm install --save-dev oxlint oxfmt
```

```json
{ "scripts": { "lint": "oxlint", "format": "oxfmt" } }
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
npm run lint
npm run test
```

Any step fail → commit blocked, AI get error message.

Bonus loop: give LLM access to running local dev server, check frontend.

## 4. Formatter — lint-staged + oxfmt

Auto-format staged file before commit.

```sh
pnpm install --save-dev lint-staged
```

`.lintstagedrc`:

```json
{ "*.{js,ts,jsx,tsx}": ["oxlint --fix", "oxfmt"] }
```

Run oxlint + oxfmt on staged file, auto-restage. All AI code match style now. One toolchain, no Prettier/ESLint.
