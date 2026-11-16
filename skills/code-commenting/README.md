# Code commenting

A reusable skill for AI coding agents that support the [Agent Skills](https://agentskills.io/specification) standard. It writes, reviews, improves, and removes comments so that code explains what and comments explain why.

The skill does not set a comment quota, and it does not document every function. It comments business rules, security decisions, algorithms, API contracts, concurrency, workarounds, and edge cases. It removes comments that repeat the code.

## Layout

```
code-commenting/
├── SKILL.md                 # workflow the agent follows
├── README.md                # this file
└── references/
    ├── examples.md          # good and bad comments
    ├── workflows.md         # one procedure per task
    ├── checklist.md         # the same eight checks, used for review
    ├── javascript-typescript.md
    ├── python.md
    ├── java.md
    ├── csharp.md
    ├── go.md
    ├── rust.md
    └── other-languages.md
```

Agents read `SKILL.md` when a task matches the description, then open a reference only when that task needs it.

## Install

This repository stores the skill at `skills/code-commenting/`. Cursor and Claude Code do not discover that catalog path. Copy the folder onto a discovery path, or symlink it where Claude Code is the consumer.

Replace `/path/to/AI_SKILLS` with the clone of this repository.

Cursor, for one project:

```bash
mkdir -p .cursor/skills
cp -R /path/to/AI_SKILLS/skills/code-commenting .cursor/skills/code-commenting
```

`.agents/skills/code-commenting/` is the other project path Cursor documents. For every project on this machine, use `~/.cursor/skills/code-commenting/` or `~/.agents/skills/code-commenting/`.

Claude Code, for one project:

```bash
mkdir -p .claude/skills
ln -s /path/to/AI_SKILLS/skills/code-commenting .claude/skills/code-commenting
```

Claude Code also accepts a real copy at that path. For every project on this machine, use `~/.claude/skills/code-commenting/`. Claude Code documents symlink support for these skill folders.

Cursor also loads `.claude/skills/`, `.codex/skills/`, `~/.claude/skills/`, and `~/.codex/skills/`. A skill installed for Claude Code is therefore visible to Cursor as well, and a second copy is unnecessary. Cursor's own docs do not state that a symlink under `.cursor/skills/` or `.agents/skills/` is supported, so those paths should be a real copy.

Start a new session after installing. In Cursor, confirm the skill under Customize → Skills. In Claude Code, type `/` and look for `code-commenting`.

## Usage

Invoke it directly:

- Cursor Agent chat: `/code-commenting`
- Claude Code: `/code-commenting`

Or ask in words that match the description. The agent should select the skill when the request is about comments or API documentation.

Three requests that match a workflow:

- "Comment the new payment retry. Explain only what the code itself does not show."
- "Review the comments in `billing/`. Do not change files."
- "Audit comment quality under `src/`. Report wrong, redundant, and missing comments. Do not edit."

The other workflows, and the steps for each, are in [references/workflows.md](references/workflows.md).

## Limits

- `skills/code-commenting/` is the source copy. Opening this repository does not by itself register the skill with Cursor or Claude Code.
- This repository does not include a Cursor plugin manifest or a marketplace package.
- The skill follows the documentation tool a project already uses. The language references are the default only when the project has not chosen one.
