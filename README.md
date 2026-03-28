# reviewing-skill

A portable Agent Skill for reviewing other skills, `SKILL.md` packages, and skill-like instruction documents.

It reviews the target with two required methodologies:
- design patterns and review principles
- "another AI uses this skill" usability and stability

It also checks all five common skill design patterns on every review:
- Tool Wrapper
- Generator
- Reviewer
- Inversion
- Pipeline

## Install

If your agent supports the Agent Skills ecosystem, install the skill with `npx skills add`:

```bash
npx skills add benyue1978/reviewing-skills
```

## When To Use It

Use this skill when you want an AI to review:
- a packaged Agent Skill
- a partial skill package
- a loose skill-like instruction document

Typical use cases:
- reviewing a new `SKILL.md` before adoption
- checking whether a skill uses the right pattern or pattern mix
- checking whether another AI could use the skill reliably without extra coaching
- finding portability or packaging problems

## How The Review Works

The review logic is intentionally strict and visible.

First, the reviewer applies two methodologies:

1. Design patterns and principles
The skill checks the target against a review rubric, including discovery quality, progressive disclosure, output constraints, loopholes, portability, and whether the structure matches the job.

2. Another-AI stability check
The skill simulates another competent AI activating the skill with no extra help. It checks whether that AI would know when to load the skill, what to read next, what order to follow, and how to produce the expected output consistently.

Then the reviewer assesses all five skill patterns explicitly:
- `Tool Wrapper`: should this skill mainly teach a library, policy, domain, or internal system?
- `Generator`: should this skill produce structured output from a template?
- `Reviewer`: does this skill need a rubric, severity model, or evidence rules?
- `Inversion`: should this skill ask structured questions before acting?
- `Pipeline`: should this skill enforce a fixed sequence of steps?

The final report always includes:
- `Findings`
- `Bottom line`
- `Suggestions`
- `Answers`
- a direct closing question naming the main suggested changes

Every finding is expected to include severity, inline file/line references, and, when useful, a short quote from the reviewed text.

## Output Style

The skill is tuned to produce reviews that read naturally instead of sounding like a rigid form.

Notable output rules:
- line references should appear inside the finding text, not only as a trailing citation
- the review should explain impact naturally rather than using the literal phrase `Why it matters:`
- if there are no issues, the skill writes `No findings.`
- the closing question should name concrete changes instead of saying only "the suggestions"

## Examples

These examples come from the skill reviewing itself during development.

Example finding about weak visible pattern reporting:

> In `SKILL.md`, the workflow said to evaluate all five design patterns, but the output contract did not force a visible per-pattern result. Another AI could comply internally and still return a review where the user could not tell whether all five patterns were actually assessed.

Example finding about loose input handling:

> The workflow said "Read the main instruction file first," but for a skill-like document there was no explicit rule for what counted as the main file. That left room for inconsistent reviews when the input was a prompt, README, or mixed notes.

Example finding about packaging checks:

> The skill promised to call out packaging gaps against the Agent Skills format, but the supporting guidance stayed at the portability-principles level and did not provide a concrete packaging checklist.

Example final state after iterating on the skill:

```md
# Findings:

No findings.

# Bottom line:


# Suggestions:

- Pattern assessment for this skill:
  - Tool Wrapper: does not apply as a core pattern.
  - Generator: applies and is already present in lightweight form.
  - Reviewer: applies and is already present as the core pattern.
  - Inversion: does not apply by default.
  - Pipeline: applies and is already present through the ordered workflow.
```

## Self-Review Was Useful

This skill was improved by using the skill to review itself multiple times.

That turned out to be useful because it exposed problems that were easy to miss while authoring:
- line references were present but buried at the end of findings
- the template used awkward section titles
- the closing question was too generic
- the rule for non-packaged inputs was underspecified
- packaging checks were too vague
- pattern reporting needed to be visible, not just implied

The final version is stronger because the skill had to survive its own review logic.

## References

Primary references:
- [5 Agent Skill Design Patterns Every ADK Developer Should Know](https://lavinigam.com/posts/adk-skill-design-patterns/)
- [Agent Skills Specification](https://agentskills.io/specification)
- [Agent Skills Best Practices](https://agentskills.io/skill-creation/best-practices)
- [Agent Skills Scripts Guide](https://agentskills.io/skill-creation/using-scripts)
- [Anthropic Claude Best Practices](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/claude-4-best-practices)

## File Layout

```text
reviewing-skill/
├── SKILL.md
├── references/
│   └── review-principles.md
└── assets/
    └── review-template.md
```

Key files:
- [`reviewing-skill/SKILL.md`](./reviewing-skill/SKILL.md): activation rules, workflow, severity, pattern review rules
- [`reviewing-skill/references/review-principles.md`](./reviewing-skill/references/review-principles.md): detailed review rubric, portability guidance, packaging sanity check
- [`reviewing-skill/assets/review-template.md`](./reviewing-skill/assets/review-template.md): exact report structure
