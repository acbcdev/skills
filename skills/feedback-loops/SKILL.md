---
name: feedback-loops
disable-model-invocation: true
description: Wire stack-agnostic feedback loops (static check, tests, formatter) behind a pre-commit gate so an agent can verify its own work
argument-hint: (run in a project root)
---

A **feedback loop** is a check that goes GREEN when the code is good and RED when it isn't, wired so the agent runs it without a human. Three loops — static check, tests, formatter — gated behind a pre-commit hook so a bad change is caught before it lands.

These are concepts, not tools. Pick whatever the stack already uses. The skill is done only when a deliberate break makes the loop go RED.

## 0. Identify the stack, confirm the loops

Read the project manifest to detect language and package manager: `package.json`, `pyproject.toml`, `Cargo.toml`, `go.mod`, `Gemfile`, etc. Ambiguous or missing → ASK the user.

Then confirm with the user before wiring (propose the stack's common choice, let them override):
- which of the three loops to wire (default: all three),
- which tool fills each, if more than one fits.

Done: stack known, tool chosen for each loop the user wants.

## 1. Static check — read the code without running it

Catches errors the code never has to execute to reveal. Types or lint, whatever the stack offers:
- types: `tsc --noEmit`, `mypy`, `pyright`, `go vet`, `cargo check`
- lint: `eslint`, `ruff`, `clippy`, `golangci-lint`

Wire it behind one command. Done: the command runs and exits 0 on clean code.

## 2. Tests — run the code and assert

The stack's test runner, in run-once mode — never watch, watch hangs a hook:
- `vitest run`, `pytest`, `cargo test`, `go test ./...`, `rspec`

Done: one command runs the suite and exits 0.

## 3. Formatter — fix style so the agent stops guessing

A tool that rewrites code to a fixed style:
- `prettier`, `ruff format` / `black`, `gofmt`, `rustfmt`

Done: running it leaves the tree formatted and exits 0.

## 4. Pre-commit gate

Install a pre-commit hook that runs the loops; any failure blocks the commit. Use whatever the stack reaches for, or a plain git hook:
- JS: husky, lefthook
- any stack: the `pre-commit` framework, lefthook, or a hand-written `.git/hooks/pre-commit`

The hook runs, in order: formatter (on staged files) → static check → tests.
Done: hook file exists and is executable.

## 5. Prove the loop goes RED

Stage a deliberate error the static check or tests will catch (a type error, a failing assert), attempt a commit, confirm it is BLOCKED, then clean up the error.

Done: the commit was blocked (RED). A loop that never goes RED is not a feedback loop — if the commit succeeds, fix the hook before finishing.
