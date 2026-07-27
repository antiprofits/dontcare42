# CLAUDE.md — Claude Operational Rules

This file governs Claude-specific behaviour in this repository.
Read `AGENTS.md` first — it contains the architecture and standards.
This file contains only what is unique to Claude.

---

## Planning Work

1. Read `AGENTS.md`, `PROJECT.md`, and the relevant `ProjectSkills/projects/*/` file before writing any code.
   Read `LESSONS.md` before starting work.
2. Confirm the task is within the current phase scope boundary defined in `AGENTS.md`.
3. If the task spans more than one file, state the change sequence before starting.
4. Do not design for hypothetical future requirements. Implement exactly what the task asks.

## Using Skills

- Check `ProjectSkills/skill-arsenal.md` before installing a new skill to avoid duplicates.
- Only install skills that map directly to work in the current phase.
- After installing a skill: update `ProjectSkills/skill-arsenal.md` and the relevant project skill file.
- Trim installed skills to `SKILL.md` only — never commit binary assets, fonts, or example files.
- Parked skills are listed in `skill-arsenal.md` with status `parked` — do not install them until the trigger condition is met.

### Parked Skills — Install Triggers

| Skill | Install when |
|-------|-------------|
| `tailwind-design-system` (wshobson/agents) | `SearchDnaPage.tsx` UI work begins (Phase 3) |
| `hyperframes` suite (heygen-com) | A video production surface is explicitly scoped |

## How to Communicate

- One-sentence updates at key moments (found something, changed direction, hit a blocker).
- End-of-turn summary: what changed and what's next. Nothing else.
- Do not narrate tool calls or internal deliberation.
- Use the reporting format from `AGENTS.md` → Communication and Reporting Format.

## When to Stop and Ask

Stop and ask before proceeding when:
- The task is out of scope per `AGENTS.md` → Scope Boundaries.
- A destructive git operation is required (force push, reset --hard, branch delete).
- A new external provider or API key is needed that is not listed in `AGENTS.md` → Provider Boundaries.
- A skill install would bring in more than the `SKILL.md` file (binary assets, examples, etc.).
- The PR diff touches a source-of-truth file (`types.ts`, `skills-lock.json`, `AGENTS.md`) in a way that changes contracts, not just adds to them.

## Validating Changes

Run the validation commands from `AGENTS.md` → Validation Commands after every non-trivial change.
If no build system exists yet, at minimum run `tsc --noEmit` on changed TypeScript files.

## Reporting Completion

A task is complete only when all items in the Definition of Done (`AGENTS.md`) are checked.
State which items passed. If any did not pass, say so and why before closing the turn.

## Git Discipline

- Branch: always develop on `claude/vercel-labs-skills-rdivww` (or the branch specified at session start).
- Commits: descriptive messages explaining the why. No co-author lines unless instructed.
- Push: after every logical unit of work — do not accumulate large uncommitted diffs.
- PR: create a draft PR after the first push if one does not exist. Never merge without user instruction.
