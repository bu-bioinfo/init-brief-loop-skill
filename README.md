# init-brief-loop

A Claude Code skill that scaffolds a **brief → execute → verify → commit**
workflow into a project repo — a lightweight, BDD-style session framework
originally built for teaching a bioinformatics course on working with
agentic coding harnesses, but generic enough for any data/analysis or
software project.

## What it does

Running the skill in a repo creates four documents:

- `CLAUDE.md` — the operating loop Claude Code follows, and the repo's
  structure map.
- `PROJECT.md` — a standing scope-doc stub (overview, core scope,
  out-of-scope, stack, data/storage) for the student's own project.
- `brief-log.md` — the session log schema and an empty log, ready for the
  first entry.
- `briefs/TEMPLATE.md` — the brief template (`Want` / `Purpose` / `Scope` /
  `Expected`), copied to `briefs/<NNN>-<slug>.md` before each session.

It's structure only — it doesn't know anything about the specific project
being built. See `SKILL.md` for exactly what the skill does step by step.

## The loop, briefly

1. **Brief** — before a session starts, write `briefs/<NNN>-<slug>.md`.
2. **Execute** — start the session by referencing the brief directly, e.g.
   `@briefs/001-my-slug.md let's do this`, rather than describing it in
   prose, so Claude works from the brief's exact text.
3. **Log** — Claude drafts a `brief-log.md` entry.
4. **Verify** — the student reads the diff and confirms/edits the log
   entry themselves; Claude's draft is never final.
5. **Commit** — one commit per session, `brief-log.md` staged alongside the
   changed files, using [Conventional Commits](https://www.conventionalcommits.org/).

Each `Expected` item in a brief is tagged `[test]` or `[manual]`:

- **`[test]`** — the behavior is critical enough to need an objective
  pass/fail check (e.g. "filters to exactly N rows"). The student
  implements and runs the test separately; Claude never runs one itself
  or claims to have.
- **`[manual]`** — requires domain-specific knowledge or judgment that
  can't be delegated to an LLM (e.g. "this plot is biologically
  plausible"). Claude lists these as pending student review in the log
  draft — it doesn't assert or describe the outcome on the student's
  behalf.

## Install

Download and extract this repo directly into a skills directory — no
Node/npm required. Choose one:

**Per-project** (only available in this repo):

```sh
mkdir -p <your-project>/.claude/skills/init-brief-loop
curl -fsSL https://github.com/bu-bioinfo/init-brief-loop-skill/archive/refs/heads/main.tar.gz \
  | tar -xz -C <your-project>/.claude/skills/init-brief-loop --strip-components=1
```

**Global** (available in every project):

```sh
mkdir -p ~/.claude/skills/init-brief-loop
curl -fsSL https://github.com/bu-bioinfo/init-brief-loop-skill/archive/refs/heads/main.tar.gz \
  | tar -xz -C ~/.claude/skills/init-brief-loop --strip-components=1
```

To update to the latest version later, just re-run the same command —
it overwrites the existing install.

(Note: this skill's `SKILL.md` references files under `templates/` in
the same directory, so installers that fetch only `SKILL.md` — such as
`npx skills add` — will not work here.)

## Use

In Claude Code, inside the target repo, ask it to set up the brief loop
(e.g. "scaffold the brief loop into this repo") — the skill's description
in `SKILL.md` is written to match on requests like that.
