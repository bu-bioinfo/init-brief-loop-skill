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

## Install

**Manual (recommended for a class):** clone this repo, then copy or
symlink it into your project's skills directory:

```sh
git clone git@github.com:bu-bioinfo/init-brief-loop-skill.git /tmp/init-brief-loop
cp -r /tmp/init-brief-loop <your-project>/.claude/skills/init-brief-loop
rm -rf <your-project>/.claude/skills/init-brief-loop/.git
```

**Via the skills CLI**, if you want it in that ecosystem:

```sh
npx skills add bu-bioinfo/init-brief-loop-skill
```

## Use

In Claude Code, inside the target repo, ask it to set up the brief loop
(e.g. "scaffold the brief loop into this repo") — the skill's description
in `SKILL.md` is written to match on requests like that.
