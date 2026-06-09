---
name: autommit
description: Automate commit messages using the Conventional Commits specification.
disable-model-invocation: true
argument-hint: (feature, files, domain)
model: claude-3-5-haiku
allowed-tools: 
    - Bash(git stash*)
    - Bash(git log*)
    - Bash(git diff*)
    - Bash(git show*)
---

Format: `<type>(<scope>): <description>`

Default strategy: `files`
## Strategies
- `file` - one commit per file
- `features` - one commit per feature across files
- `domain` - group by business domain (auth, payments, etc.)

$ARGUMENTS

Determine grouping strategy, generate conventional commit messages. Never include co-author info.

`git add <files-affected> && git commit -m "<message>"`

## Rules
- Imperative present tense ("add" not "added")
- `!` for breaking changes: `feat(api)!: change user response`
- Body only when "why" isn't obvious
