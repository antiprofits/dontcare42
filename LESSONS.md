# LESSONS.md — Candidate Learning Queue

Raw observations and unvetted lessons from completed sessions.
Items here are candidates for review, not approved facts.

**Review process:**
1. Read this file before starting work (per CLAUDE.md Planning Work step 1).
2. Evaluate each entry: accurate? still relevant? worth promoting?
3. Promote approved entries to Engram (approved operational memory) via MCP tools.
4. Remove promoted entries from this file.
5. Add new observations using aar-loop (`scripts/append_lesson.py`) at session end.

**Do not:** treat entries here as confirmed doctrine. They are unreviewed.
**Do not:** let this file grow without periodic review. It is a queue, not an archive.

---

## Queue

<!-- aar-loop appends entries below this line -->

### 2026-08-05 — Governance Backfill (Phase 0)

**Observation:** The original `skills-lock.json` (v1) recorded `computedHash` inconsistently:
for hyperframes suite skills, the hash was computed against the upstream source file, not the locally
committed file. For omni-* and task-observer, the hash matched the local committed file.
This means the v1 hash values for hyperframes suite are NOT integrity checks of the committed content.

**Lesson:** Always compute hashes from the locally committed file content, not the upstream source.
The two will differ if any transformation occurred during install (encoding, line endings, trimming).

**Status:** Recorded. Promote to Engram when Engram is configured (Phase 3).

---

### 2026-08-05 — Install SHA Gap

**Observation:** None of the skills installed before governance was established have a recorded
install-time commit SHA. The Phase 0 backfill uses current upstream HEAD SHAs as reference
snapshots only. These are NOT the exact commits from which the files were pulled.

**Lesson:** Record the exact git commit SHA at install time. This is a one-time operation that
cannot be reconstructed retroactively from the committed file content alone.

**Status:** Recorded. Promote to Engram when Engram is configured (Phase 3).

---

### 2026-08-05 — User-Level Skill Persistence

**Observation:** Skills installed to `~/.claude/skills/` in an ephemeral remote container
session are lost when the container is reclaimed. The session summary confirmed aar-loop,
beautify-github-readme, and the emilkowalski suite were installed but reset at session end.

**Lesson:** User-level skills installed in remote container sessions must be re-installed
on the local machine to persist. This is a Phase 1 prerequisite for any subsequent phase
that depends on those skills.

**Status:** Recorded. Promote to Engram when Engram is configured (Phase 3).

---

### 2026-08-05 — wshobson TypeScript Skills Gap

**Observation:** Four TypeScript skills from `wshobson/agents` were approved for user-level
install in a prior session. Their exact skill names were not captured in the governance record.
They appear in neither `skill-arsenal.md` (user-level Active section) nor `skills-lock.json`.

**Lesson:** Record skill names and SHAs at approval time, not just at install time.
Approval records must be sufficient to reconstruct the install without re-running the approval.

**Action required:** Before Phase 1, verify the skill names from local machine `~/.claude/skills/`
and add entries to `skill-arsenal.md`.

**Status:** Recorded. Action pending.

---
