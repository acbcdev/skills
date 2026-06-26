---
name: feedback-loops
disable-model-invocation: true
description: Wire stack-agnostic feedback loops (static check, tests, formatter) behind a pre-commit gate so an agent can verify its own work
argument-hint: (run in a project root)
---

A **feedback loop** = check that go GREEN when code good, RED when not, wired so agent run it without human. Three loops — static check, tests, formatter — gated behind pre-commit hook so bad change caught before land.

Concepts, not tools. Pick whatever stack already use. Skill done only when deliberate break make loop go RED.

## 0. Identify the stack, confirm the loops

Read project manifest to detect language and package manager: `package.json`, `pyproject.toml`, `Cargo.toml`, `go.mod`, `Gemfile`, etc. Ambiguous or missing → ASK user.

Then confirm with user before wiring (propose stack common choice, let them override):
- which of three loops to wire (default: all three),
- which tool fill each, if more than one fit.

Done: stack known, tool chosen for each loop user want.

## 1. Static check — read the code without running it

Catch errors code never has to run to reveal. Types or lint, whatever stack offer:
- types: `tsc --noEmit`, `mypy`, `pyright`, `go vet`, `cargo check`
- lint: `eslint`, `ruff`, `clippy`, `golangci-lint`

Wire behind one command. Done: command run, exit 0 on clean code.

## 2. Tests — run the code and assert

Stack test runner, run-once mode — never watch, watch hang hook:
- `vitest run`, `pytest`, `cargo test`, `go test ./...`, `rspec`

Done: one command run suite, exit 0.

## 3. Formatter — fix style so the agent stops guessing

Tool that rewrite code to fixed style:
- `prettier`, `ruff format` / `black`, `gofmt`, `rustfmt`

Done: running it leave tree formatted, exit 0.

## 4. Pre-commit gate

Install pre-commit hook that run loops; any failure block commit. Use whatever stack reach for, or plain git hook:
- JS: husky, lefthook
- any stack: the `pre-commit` framework, lefthook, or hand-written `.git/hooks/pre-commit`

Hook run, in order: formatter (on staged files) → static check → tests.
Done: hook file exist and executable.

## 5. Prove the loop goes RED

Stage deliberate error static check or tests will catch (type error, failing assert), attempt commit, confirm BLOCKED, then clean up error.

Done: commit blocked (RED). Loop that never go RED not a feedback loop — if commit succeed, fix hook before finishing.