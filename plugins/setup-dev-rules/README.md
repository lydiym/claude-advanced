# setup-dev-rules

A Claude Code slash command that extracts a project's **ideal state** — the maintainer's sense of beauty — and codifies it into `./dev-rules.md`.

The resulting file is **not** a description of how the code is written today (with all its tech debt and workarounds). It is a constitution for how the code **should** look in an ideal world, so that future Claude Code sessions and human contributors constantly push the "matter" of the project toward the "idea".

## Install

Place the plugin in your Claude Code plugins directory, or invoke the command directly from this repository.

## Usage

```text
/setup-dev-rules
```

The agent will:

1. **Silently scan** the repository (stack, structure, configs, code, tech debt).
2. **Open with a brief framing** of the mission.
3. **Run a code-driven Socratic dialogue** — one question per turn, every question anchored to a real or synthetic code snippet. Every rule in the output is binding; the agent never asks the maintainer to choose "hard or soft" — that is a structural choice the agent makes from context.
4. **Surface at least 3 anti-patterns** from the current code, asking the maintainer how each should be written *ideally* in the future.
5. **Finalize** by writing `./dev-rules.md` at the repository root, structured for machine readability.

## Output

`./dev-rules.md` contains, in order:

1. **The North Star (Our Ideals)** — philosophy and architectural principles.
2. **Rules** — one universal list. Every rule takes one of four forms:
   - **Form A** — anti-pattern only, no ideal shown.
   - **Form B** — anti-pattern + ideal (the default when a paired example is meaningful).
   - **Form C** — ideal only, no specific anti-pattern.
   - **Form D** — free-form rule expressed as prose, for multi-sentence rules where the bullet+snippet structure would lose meaning.
3. **Self-Check Before You Commit** — a checklist future Claude sessions must pass.

There is no Provenance section in the file. Git history is the canonical provenance — `git log dev-rules.md` shows every change, and the commit message describes what was added or revised. Keeping the file a clean constitutional artifact beats embedding a changelog inside it.

## Re-running

Run `/setup-dev-rules` again any time the project's ideals mature. If `./dev-rules.md` already exists, the agent will read it, mention its contents, and ask whether to replace, merge, or extend it.

## Files

- `commands/setup-dev-rules.md` — the slash command definition (the agent's full system prompt).
- `.claude-plugin/plugin.json` — the plugin manifest.
