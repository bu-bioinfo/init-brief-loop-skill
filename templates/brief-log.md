# Session log

Each entry documents one session: what was asked, what
changed, and why. Every commit must have a corresponding
entry here.

**Student responsibility:** Claude drafts the `Changed` field,
but you must read the diff and edit/confirm it before
committing. This is the verification step.

## Schema

| Field    | Description |
|----------|-------------|
| #        | Sequential session number, zero-padded |
| Brief    | Link to `briefs/<NNN>-<slug>.md` |
| Expected | Copied from the brief verbatim, including `[test]`/`[manual]` tags — what should be true after this session |
| Changed  | Student-confirmed list of what actually changed and why. `[test]` items are reported passing/failing based on an actual run; `[manual]` items are listed as "pending student review," never characterized |
| Rationale | Required whenever the session made a nontrivial decision. One paragraph: what was decided and what informed it. When the decision was filling a gap the brief left open, say so explicitly — separate what the brief specified from what Claude decided on its own. Omit when there was no decision to justify. |
| Fix      | — / manual / follow-up |

## Log

---

### 001 — [date] — [title]

**Brief:** `briefs/001-<slug>.md`

**Expected:**
<!-- Copied from the brief's Expected field -->

**Changed:**
<!-- Claude drafts; student reads the diff and confirms before committing -->
- `[file]` — [what changed and why]

**Rationale:**
<!-- Required whenever a nontrivial decision was made (a real
     tradeoff was weighed, not just requested work carried out).
     One short paragraph: what was decided and what informed it.
     Omit if there was no decision to justify. -->

**Fix:**

---
