# [Skill Name] — Project Skill

> Copy this template when registering a skill scoped to a single project.
> Fill in every field. Delete this instruction block before committing.

---

## Identity

| Field | Value |
|-------|-------|
| **Skill name** | `skill-name` |
| **Source** | `owner/repo` or `local` |
| **Install path** | `.claude/skills/skill-name/SKILL.md` |
| **Lock hash** | `abc12345` |
| **Status** | `active` / `parked` / `deprecated` |
| **Scope** | `SEARCHDNA` / `Vault` / `NotchOS` / `Vantage` |
| **Added** | YYYY-MM-DD |
| **Version** | `1.0.0` or commit SHA |

---

## Purpose

One sentence: what specific problem in this project does this skill solve?

---

## Trigger Conditions

Specific conditions within this project that should invoke this skill.

- When working on `lib/<project>/…`
- When the user asks about …
- Do not use for …

---

## Pipeline Position

Where does this skill sit in the project's dependency graph?
Reference `ProjectSkills/dependency-map.md`.

```
upstream-step
    ↓
[this skill]
    ↓
downstream-step
```

---

## Global Skills Used

List any global skills this project skill depends on or composes with.

- `global-skill-name` — how it's used here

---

## Customisations

Any project-specific prompt additions, constraints, or overrides.
If none: write "None."

---

## Validation

- [ ] Works correctly against Phase N test data
- [ ] Output conforms to `lib/<project>/types.ts` schema
- [ ] Listed in `ProjectSkills/skill-arsenal.md`
- [ ] Listed in `ProjectSkills/projects/<project>/<project>-Skills.md`

---

## Deprecation Notes

If deprecated: reason and replacement.
If active: "N/A."
