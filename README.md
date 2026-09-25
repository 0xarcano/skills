# Arcano Agent Skills

Portable [Agent Skills](https://agentskills.io/specification) for AI coding agents (Cursor, Claude Code, Codex, and others that load `SKILL.md`).

Each skill is a folder under `skills/` with a `SKILL.md` (YAML frontmatter + instructions) and optional `scripts/`, `references/`, and `assets/`.

## Layout

```text
skills/                    # published catalog (one folder per skill)
  <skill-name>/
    SKILL.md
    scripts/               # optional
    references/            # optional
    assets/                # optional
templates/skill/           # starter for new skills
.cursor/skills/            # in-repo authoring help only (not catalog)
.cursor/rules/             # repo conventions for agents
```

Catalog skills live in **`skills/`**, not `.agents/skills/` or `.cursor/skills/`, so editing this repo does not inject every skill description into the agent context.

## Add a skill

1. Copy the template:

   ```bash
   cp -R templates/skill skills/my-skill-name
   ```

2. Rename the folder to match the skill `name` (lowercase, hyphens, max 64 chars).

3. Edit `skills/my-skill-name/SKILL.md`:
   - Set `name` to the folder name
   - Write a third-person `description` with **what** the skill does and **when** to use it
   - Keep the body concise; put long reference material in linked files one level deep

4. Add optional `scripts/`, `references/`, or `assets/` as needed.

## Quality checklist

- [ ] `name` matches the parent folder (lowercase letters, numbers, hyphens only)
- [ ] `description` includes WHAT and WHEN, written in third person
- [ ] `SKILL.md` body stays under ~500 lines; use progressive disclosure for detail
- [ ] File links from `SKILL.md` are one level deep
- [ ] Terminology is consistent throughout
- [ ] Scripts document how to run them and required packages

## Install a skill

Copy or symlink a skill folder into an agent skills root:

| Scope | Cursor | Agents / Claude-compatible |
| ----- | ------ | -------------------------- |
| User | `~/.cursor/skills/<name>/` | `~/.agents/skills/<name>/` or `~/.claude/skills/<name>/` |
| Project | `.cursor/skills/<name>/` | `.agents/skills/<name>/` |

Example:

```bash
ln -s "$(pwd)/skills/my-skill-name" ~/.cursor/skills/my-skill-name
```

Installers that discover a `skills/` catalog (for example `npx skills add`, `gh skill install`, or skills-pm) can target this repository when those tools are available:

```bash
# examples — exact flags depend on the CLI
npx skills add 0xarcano/skills --skill my-skill-name
gh skill install 0xarcano/skills my-skill-name --agent cursor
```

## License

MIT — see [LICENSE](LICENSE).
