---
name: init-brief-loop
description: Scaffold the brief -> execute -> verify -> commit workflow (brief template, session log, CLAUDE.md operating loop, project scope doc) into a new or existing repo. Use when a student or instructor wants to set up this BDD-style session framework for a new project, port it from another repo, or is starting a course project that should follow the brief/log cycle from day one.
---

# Init Brief Loop

Scaffolds the reusable core of the brief -> execute -> verify -> commit
framework into a repo: `CLAUDE.md`'s operating loop, `briefs/TEMPLATE.md`,
`brief-log.md`'s schema, and a `PROJECT.md` scope-doc stub. This is
structure only — it does not know anything about the specific project a
student is building. Content (what the project does, its stack, its first
brief) is theirs to fill in.

## What the loop is, briefly

Every session in a repo using this framework follows the same five steps:
1. **Brief** — write `briefs/<NNN>-<slug>.md` (Want / Purpose / Scope /
   Expected) before work starts.
2. **Execute** — start the session by referencing the brief directly with
   `@briefs/<NNN>-<slug>.md` in the prompt, not by describing it in prose,
   so Claude works from the brief's exact text.
3. **Log** — Claude drafts an entry in `brief-log.md`.
4. **Verify** — the student reads the diff and confirms/edits the log
   entry themselves; Claude's draft is never final.
5. **Commit** — one commit per session, `brief-log.md` staged alongside the
   changed files, Conventional Commits message.

Don't just recite this back to the student — actually perform the steps
below to put it in place.

## Steps

1. **Determine the target directory.** Default to the current working
   directory. If it already looks like an established, unrelated project
   (existing source tree, unrelated `CLAUDE.md`), confirm with the user
   before scaffolding into it rather than assuming it's the intended
   target.

2. **Check for collisions.** For each of `CLAUDE.md`, `PROJECT.md`,
   `brief-log.md`, `briefs/TEMPLATE.md`, `README.md` in the target
   directory: if it already exists, do not overwrite it silently. Show the
   user what's there and ask whether to leave it, merge in the missing
   pieces (e.g. append the operating-loop section to an existing
   `CLAUDE.md`), or replace it. If it doesn't exist, create it from the
   matching template below.

3. **Copy the templates**, from this skill's `templates/` directory into
   the target repo:
   - `templates/CLAUDE.md` -> `<target>/CLAUDE.md`
   - `templates/PROJECT.md` -> `<target>/PROJECT.md`
   - `templates/brief-log.md` -> `<target>/brief-log.md`
   - `templates/briefs-TEMPLATE.md` -> `<target>/briefs/TEMPLATE.md`
     (create the `briefs/` directory if it doesn't exist)
   - `templates/README.md` -> `<target>/README.md` (only if no README
     exists — otherwise offer to append its "Where to look" table to the
     existing one instead of replacing it)

4. **Report what was created**, and point out the placeholder brackets
   (`[...]`) left in `CLAUDE.md` (What this repository is, Commands) and
   `PROJECT.md` (Overview, Core scope, Out of scope, Stack & tooling, Data
   & storage) that the student still needs to fill in — the skill scaffolds
   structure, not project content.

5. **Tell the student the next step**: copy `briefs/TEMPLATE.md` to
   `briefs/001-<slug>.md`, fill in Want/Purpose/Scope/Expected for their
   first real unit of work, then start that session by typing something
   like `@briefs/001-<slug>.md let's do this` — referencing the brief file
   directly rather than re-describing it in prose.

## Boundaries

- This skill never touches application/analysis code, data files, or
  git history — only the four framework documents above.
- It doesn't pick a session number or write a brief on the student's
  behalf — the first brief is the student's own work, same as every
  session after it.
- If the repo already has a `brief-log.md` with entries (i.e. the loop is
  already running here), there's nothing to scaffold — say so instead of
  re-initializing it.
