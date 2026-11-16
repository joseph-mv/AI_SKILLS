# Contributing

Add and update skills in `skills/`. Each skill is one folder that follows the [Agent Skills specification](https://agentskills.io/specification).

## Add a skill

1. Create `skills/<skill-name>/`.
2. Copy [`templates/SKILL-template.md`](templates/SKILL-template.md) to `skills/<skill-name>/SKILL.md`.
3. Delete the note at the top of the template. Do not commit those authoring instructions into `SKILL.md`.
4. Set the frontmatter, then remove any body sections the skill does not need.
5. Add a line for the skill in the skills directory in [`README.md`](README.md).

Use one skill per folder. Do not overwrite another skill’s files. When you edit a skill, preserve its existing content and change only what the update requires.

## `SKILL.md`

Every skill folder needs a `SKILL.md` file with YAML frontmatter and Markdown instructions.

Required fields:

- `name` — must match the parent directory name. Use 1–64 characters: lowercase letters, digits, and hyphens only. Do not start or end with a hyphen, and do not use consecutive hyphens (`--`).
- `description` — 1–1024 characters. Say what the skill does and when to use it, including keywords an agent can match.

Add `license`, `compatibility`, `metadata`, or `allowed-tools` only when they apply. `compatibility` is at most 500 characters. `allowed-tools` is experimental: a space-separated list of tools.

Keep `SKILL.md` under 500 lines. Put longer material in `references/` and link to it with a path relative to the skill root, one level deep from `SKILL.md`.

## Optional folders

Create these only when the skill uses them:

- `scripts/` — executable code. Keep scripts self-contained, or state their dependencies, and include clear error messages.
- `references/` — documentation the agent reads on demand.
- `assets/` — templates, images, and other static files.

Do not add empty copies of these folders.

## Update the directory

After adding, renaming, or removing a skill, update its line in the README skills directory:

```markdown
- [`skills/skill-name/`](skills/skill-name/) — What the skill does and when to use it.
```

The folder name, the `name` field, and the directory entry must stay in sync.
