# Glowplug skills

Free, public, Apache-2.0-licensed agent skills for Supacharger, Specdrive and other projects. Skills are instructions and optional supporting files, not paid application modules.

## Catalogue

- `general/changelog`: curated, evidence-based release notes.
- `general/handhold-me`: feature proposals, implementation checklists, and guided delivery without a prescribed technology stack.
- `specdrive/specdrive-handhold-me`: Specdrive feature proposals and guided delivery with project-specific safeguards.
- `supacharger/`: reserved for future Supacharger skills.

Each skill lives at `<category>/<skill-name>/SKILL.md` with YAML `name` and `description`. The name matches the directory. Supporting `references/`, `scripts/` and `assets/` belong inside that skill only when needed. Register installable skills in `catalogue.json`; identifiers are category/name pairs and destination names must be unique across the catalogue. Keep public descriptions concise and plain text.

## Install in a project

With the Supacharger CLI feature containing public skills support:

```bash
supacharger skills install
supacharger skills install general/changelog
supacharger skills update general/changelog
```

The first command offers checkboxes. Named commands work without a terminal prompt. Installed folders live in `.agents/skills/`; `.supacharger/skills-lock.json` records repository, immutable commit and file hashes. Commit both to the application repository. Existing untracked installations and local edits are never silently overwritten. Core updates do not update skills.

For a reviewed source revision, use `--ref <commit-or-tag>`. Maintainers can test a committed local catalogue with `--source /path/to/glowplug-skills`; the installer exports the committed revision, not uncommitted files. Publish the recorded revision before expecting other developers to retrieve it from GitHub.

Installing the changelog skill does not grant permission to edit Supacharger Core history or commit changes. Repository instructions supply those policies. This source checkout is separate from project installations.
