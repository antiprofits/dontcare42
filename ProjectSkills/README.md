# ProjectSkills — Skill Package Manager

This directory is the versioned registry for all Claude skills in this repository.
Skills are treated as managed dependencies — not scattered prompt files.

---

## Structure

```
ProjectSkills/
├── README.md              # This file
├── skill-arsenal.md       # Global inventory of every skill ever added
├── dependency-map.md      # Pipeline and skill dependency graphs
├── changelog.md           # Version history of skill changes
├── templates/
│   ├── Global-Skill.md    # Template: skills used across all projects
│   └── Project-Skill.md   # Template: skills scoped to one project
└── projects/
    ├── SEARCHDNA/         # Demand Intelligence module
    ├── Vault/
    ├── NotchOS/
    └── Vantage/
```

---

## How Skills Are Managed

Skills are installed via the `skills` CLI and land in `.claude/skills/<name>/SKILL.md`.
The `skills-lock.json` at the repo root tracks source, version hash, and path.

**Rules:**
- Only `SKILL.md` files are committed. No binary assets, fonts, or example files.
- Every install or removal must update `skill-arsenal.md`.
- Every project-scoped skill must be listed in the relevant `projects/<name>/<name>-Skills.md`.
- Parked skills are tracked in `skill-arsenal.md` with status `parked` — not installed until the trigger fires.

---

## Skill Status Values

| Status | Meaning |
|--------|---------|
| `active` | Installed and available in this session |
| `parked` | Identified as useful but not yet installed; has a named trigger condition |
| `deprecated` | Previously active, removed; tracked for provenance |
| `global` | Installed at user level (`~/.claude/skills/`), not in this repo |

---

## Adding a New Skill

1. Run `npx -y skills add <source> --skill <name> --agent claude-code`
2. Trim to `SKILL.md` only: `find .claude/skills/<name> -not -name "SKILL.md" -delete`
3. Update `ProjectSkills/skill-arsenal.md` — add a row with source, version hash, status, and scope
4. Update the relevant `projects/<name>/<name>-Skills.md`
5. Update `ProjectSkills/dependency-map.md` if the skill fits into a pipeline
6. Commit `skills-lock.json`, the `SKILL.md`, and the updated registry files together
