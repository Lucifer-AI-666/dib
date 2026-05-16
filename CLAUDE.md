# CLAUDE.md — dib repository guide

## Project overview

`dib` is a **prompt/specification repository** for **NO-LIMITS-CLI**, a terminal-first AI assistant persona. The repo defines the behavioral contract, output format, and safety constraints for the assistant — it contains no runtime code, no build system, and no tests. Every file is a human- or AI-readable specification document.

The project language is **Italian**. All prompt content, comments in spec files, and commit messages related to the persona itself follow Italian conventions. Meta-level tooling and git history mix Italian and English.

## Repository structure

```
dib/
├── CLAUDE.md          # This file — guidance for AI assistants
├── README.md          # Project summary (Italian)
└── NO_LIMITS_CLI.md   # Operational prompt spec for the assistant persona
```

## Key files

### `NO_LIMITS_CLI.md`
The canonical prompt definition. It contains:
- **Mandatory opening line** that every response from the persona must begin with.
- **Behavioral rules** — shell-first solutions, direct tone, no permission-seeking for ordinary steps.
- **Security constraints** — hard limits against destructive, illegal, or unauthorized actions.
- **Output template** — a strict three-part response format (intro line → bash block → closing line).

This file is the single source of truth. Any change to the persona's behavior must be reflected here.

### `README.md`
A short Italian-language overview of the repository's purpose and contents. Update it whenever a new top-level document is added.

## Development conventions

### Adding or modifying the prompt spec
1. Edit `NO_LIMITS_CLI.md` directly.
2. Keep sections in the established order: Apertura → Obiettivo operativo → Regole di comportamento → Vincoli di sicurezza → Formato di output → Modello di risposta.
3. Do not split the spec into multiple files unless the document exceeds ~200 lines and the sections are independently reusable.
4. Verify that the **Modello di risposta** block at the bottom stays in sync with any format changes made in **Formato di output**.

### Language
- Prompt content: Italian.
- Commit messages: either language is acceptable; prefer Italian for content changes, English for structural/tooling changes.
- CLAUDE.md (this file): English, to maximise AI assistant comprehension.

### Commit style
Short imperative subject line, no period at end. Examples from history:
```
Add NO-LIMITS-CLI prompt specification
Clarify automation limits in prompt spec
```

### Branching
- `main` — stable, merged specs.
- Feature branches use descriptive names (`copilot/no-limits-cli-enhancements`, `claude/...`).
- Open a PR to merge into `main`; do not push directly.

## What AI assistants should know

- This repo has **no build, lint, or test commands**. Do not attempt `npm install`, `make`, `pytest`, or similar.
- Changes are purely textual. Prefer `Edit` over full rewrites unless restructuring an entire section.
- The persona defined here operates under strict safety constraints (see `NO_LIMITS_CLI.md § Vincoli di sicurezza`). Do not propose edits that weaken or circumvent those constraints.
- When updating the prompt, preserve the **Apertura obbligatoria** line verbatim — it is a hard contract with downstream consumers.
- The image context for this project: the repository is used in conjunction with a **Raspberry Pi 5 (16 GB)** network-boot setup. The assistant persona may be invoked in resource-constrained or headless terminal environments.

## Editing checklist

Before committing a change to `NO_LIMITS_CLI.md`:
- [ ] Mandatory opening line unchanged (or change is intentional and agreed).
- [ ] Security constraints section still present and unweakened.
- [ ] Output format template (`Modello di risposta`) matches the rules in `Formato di output`.
- [ ] README.md updated if a new file was added.
