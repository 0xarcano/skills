---
name: skill-authoring
description: >-
  Create and edit Agent Skills in this repository. Use when adding a new skill
  under skills/, updating SKILL.md frontmatter or body, copying the skill
  template, or asking about skill structure, descriptions, or progressive
  disclosure in this catalog.
---

# Skill authoring (this repo)

## Where skills go

- **Catalog skills**: `skills/<skill-name>/SKILL.md`
- **Starter template**: `templates/skill/SKILL.md`
- **Do not** put catalog skills in `.agents/skills/` or `.cursor/skills/` unless intentionally making them active for this workspace only

Folder name must match the frontmatter `name` (lowercase letters, numbers, hyphens; max 64 chars).

## Create a new skill

1. Copy the template:

   ```bash
   cp -R templates/skill skills/<skill-name>
   ```

2. Edit `skills/<skill-name>/SKILL.md`:
   - Set `name` to `<skill-name>`
   - Write `description` in third person with WHAT and WHEN (trigger terms)
   - Keep `disable-model-invocation: true` unless the skill should auto-apply from ambient context
   - Replace stub sections with concise instructions

3. Add optional `scripts/`, `references/`, or `assets/` only when needed. Link them from `SKILL.md` one level deep.

## Description rules

- Third person (injected into the system prompt)
- Specific capabilities + when to apply
- Max 1024 characters

Good: `Extract text and tables from PDFs. Use when the user mentions PDFs, forms, or document extraction.`

Bad: `Helps with documents.`

## Authoring principles

- Assume the agent is already capable; only add domain-specific or repo-specific knowledge
- Keep `SKILL.md` under ~500 lines; put long detail in linked files
- Prefer one clear default over listing many options
- Avoid time-sensitive “before date X” instructions; use a deprecated section if needed
- Use consistent terminology throughout

## Checklist before finishing

- [ ] Path is `skills/<name>/` and `name` matches the folder
- [ ] Description has WHAT + WHEN, third person
- [ ] Body is concise; references are one level deep
- [ ] Optional scripts document run commands and dependencies
- [ ] Catalog skill is not under `.cursor/skills/` or `.agents/skills/`
