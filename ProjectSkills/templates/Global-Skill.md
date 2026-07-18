# [Skill Name] — Global Skill

> Copy this template when registering a skill that applies across all projects.
> Fill in every field. Delete this instruction block before committing.

---

## Identity

| Field | Value |
|-------|-------|
| **Skill name** | `skill-name` |
| **Source** | `owner/repo` |
| **Install path** | `.claude/skills/skill-name/SKILL.md` |
| **Lock hash** | `abc12345` (first 8 chars from `skills-lock.json`) |
| **Status** | `active` / `parked` / `deprecated` |
| **Scope** | `global` |
| **Added** | YYYY-MM-DD |
| **Version** | `1.0.0` or commit SHA |

---

## Purpose

One sentence: what problem does this skill solve and when should an agent reach for it?

---

## Trigger Conditions

List the specific conditions under which an agent should invoke this skill.
Be precise — vague triggers cause over-use.

- When …
- When the user asks for …
- Never use when …

---

## Projects Using This Skill

| Project | Usage context |
|---------|--------------|
| SEARCHDNA | … |
| Vault | … |

---

## Dependencies

List any skills or pipeline steps this skill depends on, or that depend on it.
Reference `ProjectSkills/dependency-map.md` for the full graph.

```
upstream-skill
    ↓
[this skill]
    ↓
downstream-skill
```

---

## Validation

How to confirm this skill is working correctly:

- [ ] `SKILL.md` present at install path
- [ ] Entry present in `skills-lock.json`
- [ ] Entry present in `ProjectSkills/skill-arsenal.md`
- [ ] Listed in all relevant `projects/*/`-Skills.md files

---

## Customisations

Any project-specific customisations or overrides applied to the base skill.
If none: write "None."

---

## Deprecation Notes

If status is `deprecated`, explain why it was removed and what replaced it.
If active: write "N/A."
