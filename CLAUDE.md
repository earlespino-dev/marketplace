# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

`earl-marketplace` is a **Claude Code plugin marketplace** — a content repository, not an application. There is no build, lint, or test tooling; "code" here is JSON manifests plus Markdown skill definitions and reference data. Validation is functional: install the marketplace locally and exercise the skills.

## Layout & manifest chain

The marketplace resolves through a three-level manifest chain — keep them in sync when adding or renaming things:

1. `.claude-plugin/marketplace.json` — top-level manifest. Lists each plugin with a relative `source` path (e.g. `./hood-2-coast`).
2. `<plugin>/.claude-plugin/plugin.json` — per-plugin manifest (name, version, description, keywords).
3. `<plugin>/skills/<skill-name>/SKILL.md` — one skill per directory; the YAML frontmatter `name` + `description` is what Claude reads to decide when to trigger the skill.

The `description` in `marketplace.json`, `plugin.json`, and each `SKILL.md` frontmatter overlap heavily and are duplicated intentionally — update all relevant copies together.

## Testing changes locally

```sh
claude plugin marketplace add /Users/earlespino/projects/marketplace
claude plugin install hood-2-coast@earl-marketplace
```

After editing, re-sync and reload:

```sh
claude plugin marketplace update earl-marketplace
# then restart Claude Code, or run /reload-plugins
```

## Skill authoring conventions (hood-2-coast)

These patterns are load-bearing across the existing skills — match them in any new skill:

- **`${CLAUDE_PLUGIN_ROOT}`** is the only correct way to reference bundled files (the PDF, `references/leg-data.md`, `assets/*` templates). Never hardcode paths into the plugin directory; it makes the plugin non-portable.
- **Two-tier reference data.** Cheap, transcribed Markdown (`references/leg-data.md`, `references/handbook-index.md`) is the fast path for most lookups; the bundled `references/2026-HTC-Handbook.pdf` is the source of truth read only when exact wording / GPS / page-level detail is needed. New skills should prefer the cheap tier and cite the PDF page for authoritative detail.
- **Per-user state lives in the user's Obsidian vault, not in the plugin.** Two configs persist across conversations: `<vault_path>/htc-trainer-config.md` (per-runner, owned by `htc-setup`) and `<vault_path>/htc-team-config.md` (per-team, owned by `htc-logistics`). Other skills *read* these; only the owning skill *writes* them. Keeping state in the vault is what makes the plugin reusable across different people — don't move state into the plugin directory.
- **Skill dependencies.** `htc-setup` bootstraps the runner config that `htc-trainer`, `htc-legs`, and `htc-packing` depend on; a skill that needs config but finds none should hand off to `htc-setup` first. Cross-references between skills are by skill name in prose.
- **Templates** live in each skill's `assets/` dir and are filled, not edited in place.

## Domain facts worth not re-deriving

- **Leg derivation:** 12-person team → runner N runs legs N, N+12, N+24. 8/10-person teams break that formula and must use the handbook rotation table (PDF p.16).
- **Night gear (6:00pm–7:00am, strictly enforced):** which legs are "night" depends on the team's assigned start time, *not* the leg number — always compute from the schedule.

## Note

The untracked `doc/` directory is generated PDF-viewer scaffolding (pdf.js assets), not part of the marketplace — do not commit it or treat it as source.
