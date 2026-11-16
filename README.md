# AI_SKILLS

A catalog of custom skills for AI coding agents that support the [Agent Skills](https://agentskills.io/specification) open standard.

Each skill is a folder with a `SKILL.md` file. Agents read `name` and `description` to decide when a skill applies, load the full instructions only when a task matches, and open bundled files only when those instructions ask for them.

## Repository layout

```
AI_SKILLS/
├── README.md
├── CONTRIBUTING.md
├── templates/
│   └── SKILL-template.md
└── skills/
    └── <skill-name>/
        ├── SKILL.md          # required
        ├── scripts/          # optional
        ├── references/       # optional
        └── assets/           # optional
```

Create `scripts/`, `references/`, or `assets/` only when a skill uses them.

## Skills directory

No skills have been added yet.

When you add one, list it here as a single line: the skill folder, then a short description of what it does and when to use it.

```markdown
- [`skills/skill-name/`](skills/skill-name/) — What the skill does and when to use it.
```

## Usage

1. Copy [`templates/SKILL-template.md`](templates/SKILL-template.md) to `skills/<skill-name>/SKILL.md`.
2. Set `name` to the directory name. Use 1–64 characters: lowercase letters, digits, and hyphens. Do not start or end with a hyphen, and do not use consecutive hyphens.
3. Write a `description` that says what the skill does and when to use it, including the keywords an agent should match.
4. Remove the template note at the top, and delete any body sections the skill does not need.
5. Add `scripts/`, `references/`, or `assets/` only for files that `SKILL.md` references.
6. Add a line for the skill in the directory above.

Agents that follow the standard load any directory that contains `SKILL.md`. The template is named `SKILL-template.md` so it is not discovered as a skill.

See [CONTRIBUTING.md](CONTRIBUTING.md) for how to add and maintain skills.
