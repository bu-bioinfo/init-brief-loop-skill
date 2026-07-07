# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repository is

[Describe your project here — what it does, what data or inputs it works with, and what "done" looks like for a typical session. Delete this bracket once filled in.]

Work in this repository follows a brief → execute → verify → commit loop (below) rather than being done ad hoc.

## The operating loop (read this before making any change)

Every unit of work in this repo follows the same loop:

1. **Brief.** Before a session starts, write `briefs/<NNN>-<slug>.md` from `briefs/TEMPLATE.md`: `Want` (one sentence — what should be true after), `Purpose` (why it matters — the reason it's worth doing, not user-story "as a" framing), `Scope` (files/scripts/data expected to change), `Expected` (the checkable outcome — for a single run or analysis step, use `Given`/`When`/`Then`; for a decision or design question, describe the resolved decision instead). Session numbers are sequential and zero-padded; check `briefs/` and `brief-log.md` for the highest existing number before picking the next one.
2. **Execute.** Start the session by referencing the brief file directly with `@briefs/<NNN>-<slug>.md` in your prompt to Claude Code — not by describing it in prose. This loads the brief's exact text into context instead of a paraphrase, so Claude works from what was actually written rather than a secondhand summary of it. Claude does the work described in the brief, bounded by its Scope.
3. **Log.** Claude adds an entry to `brief-log.md` following its own schema (`#`, `Brief` link, `Expected` copied verbatim from the brief, a draft `Changed` field, and `Rationale` whenever the session made a nontrivial decision).
4. **Verify.** Read the diff and edit/confirm `Changed` yourself. Do not treat Claude's draft of `Changed` as final — it's a proposal for you to correct.
5. **One commit per session.** `brief-log.md` is staged in the same commit as the changed files — never split the log entry into a separate commit. Commit messages follow [Conventional Commits](https://www.conventionalcommits.org/): `type: description` or `type(scope): description` (e.g. `docs:`, `feat:`, `fix:`, `chore:`, `refactor:`) — pick the type that matches what the session actually did, not which file it happened to touch.

## Commands

[Fill in once your project has them: install, run, lint, full test suite, single-test invocation. Don't guess at these before they exist.]

## Structure

- `brief-log.md` — source of truth for the commit workflow and the session log schema. Read it in full before changing the loop described above; this file only summarizes it.
- `briefs/TEMPLATE.md` — the brief template (`Want`/`Purpose`/`Scope`/`Expected`); copy it to `briefs/<NNN>-<slug>.md` for each session.
- `briefs/` — one file per session, plus `TEMPLATE.md`.
- `PROJECT.md` — standing scope document for this project (features, out-of-scope, stack, data/storage decisions). Briefs should point back to it rather than restating it.
