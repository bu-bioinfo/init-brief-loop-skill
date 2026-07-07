# Want
[one sentence — what should be true after this session]

# Purpose
[why this matters — what question it answers or what it enables. Not "as a user" framing; just the reason this is worth doing.]

# Scope
- [files / scripts / data expected to change]

# Expected
[If this brief describes a single run or analysis step with a checkable outcome, use Given/When/Then. Tag each Then line [test] or [manual]:
- [test]: has an objective pass/fail criterion (e.g. "filters to exactly N rows"). The test itself is implemented and run by the student, separately — Claude never runs or claims to have run it.
- [manual]: requires domain-specific judgment that can't be delegated to an LLM (e.g. "this plot looks biologically plausible"). Always ends up pending student review.]

- Given: [input data / starting state]
- When: [the step or analysis that runs]
- Then: [test] [checkable outcome with an objective pass/fail criterion]
- Then: [manual] [outcome that requires a human to look and judge]

[If this brief is a decision or design question instead (e.g. "pick a storage format"), skip Given/When/Then and just describe what the resolved decision should look like — tags don't apply.]

[Tags are set here, at brief-writing time, by the student. Claude does not retag an item during execution — e.g. deciding "the file exists" satisfies a [manual] item about whether its contents look right.]

---
Start the session by referencing this file directly, e.g. `@briefs/<NNN>-<slug>.md let's do this` — not by describing it in prose — so Claude works from the brief's exact text instead of a paraphrase.
