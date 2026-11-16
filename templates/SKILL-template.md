> Delete this note after copying this file to `skills/<skill-name>/SKILL.md`.
>
> `name` must match the directory name. Use 1–64 characters: lowercase letters, digits, and hyphens only. Do not start or end with a hyphen, and do not use consecutive hyphens (`--`).
>
> Optional frontmatter. Copy a field into the block below only when the skill needs it:
>
> ```yaml
> license: Apache-2.0
> compatibility: Requires git and network access
> metadata:
>   author: your-name
>   version: "1.0"
> allowed-tools: Bash Read
> ```

---
name: skill-name
description: What this skill does and when to use it. Include the keywords an agent should match.
---

# Skill title

## Instructions

Step-by-step instructions the agent should follow.

Keep this file under 500 lines. Move long reference material into `references/` and link to it from here.

## Examples

Show typical inputs and the outputs or actions the agent should produce.

## Edge cases

Call out situations the agent should handle differently, and what to do when information is missing.

## Resources

Create these directories only when this skill uses them. Link to files with paths relative to the skill root, and keep each reference one level deep from `SKILL.md`.

- `scripts/` — executable code the agent can run. Keep each script self-contained, or state what it depends on, and include clear error messages.
- `references/` — documentation the agent reads only when needed, such as `references/REFERENCE.md`.
- `assets/` — static resources such as templates, images, and data files.

See [the reference](references/REFERENCE.md) for details.

Run the helper:

```
scripts/run.sh
```
