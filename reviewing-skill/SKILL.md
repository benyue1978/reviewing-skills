---
name: reviewing-skill
description: Use when reviewing an agent skill, SKILL.md package, or skill-like instruction document for design quality, missing patterns, portability, or agent usability before adoption or revision
---

# Reviewing Skill

Review the target as a portable Agent Skills artifact when possible. If the target is only a skill-like instruction document, still review it and separately call out packaging gaps against the Agent Skills format.

## Review Goal

Produce a concrete review that:
- finds real issues, not generic advice
- checks whether the skill uses the right design pattern or pattern mix
- checks whether another AI could use the skill correctly and stably
- recommends any missing design pattern from the five-pattern set when it would improve the skill
- follows the required output template exactly

Load `references/review-principles.md` before writing the review.
Load `assets/review-template.md` before writing the final report.

## Required Methodologies

Use both review methodologies every time:

1. **Design patterns and principles**
Check the skill against the review principles and all five design patterns:
- Tool Wrapper
- Generator
- Reviewer
- Inversion
- Pipeline

2. **Another AI usability and stability**
Imagine a competent AI activates the skill with no extra human coaching. Check whether that AI would:
- know when to use the skill
- know what file or resource to load next
- know what order to follow
- produce the required output shape
- avoid ambiguous or unstable behavior

## Required Workflow

1. Identify the review target.
2. Determine whether it is:
- a packaged Agent Skill
- a partial skill package
- a skill-like instruction document
3. If the target follows the official skill structure, read `SKILL.md` first. If it does not, use the document the user identified as the review target.
4. Read only the additional references, assets, or scripts needed to evaluate the skill.
5. Review the target using both required methodologies.
6. Evaluate all five design patterns, even if the target currently uses none of them.
7. Recommend any pattern that should be added, removed, or made more explicit.
8. Write findings with severity and file/line references.
9. Render the final report using the template exactly.
10. End by asking whether the user wants to implement the concrete changes you recommended.

## Severity Rules

- **High**: likely to cause the AI to misuse the skill, skip required behavior, produce wrong output, or fail unpredictably
- **Medium**: meaningfully reduces review quality, portability, or reliability, but the skill may still work in some cases
- **Low**: clarity, maintainability, or optimization issue with limited direct behavior risk

Do not inflate severity. Prefer fewer, sharper findings over long weak lists.

## File And Line References

Every finding must include:
- severity
- explanation of the issue
- file path
- line number or the closest precise location available

Prefer embedding the location directly into the sentence, for example by naming the file, line number, and a short quoted phrase from the reviewed text. Do not hide all location detail at the end of the bullet.

If the target lacks file structure, cite the best available location description and say that exact line references are unavailable.

## Pattern Review Rules

Always evaluate each pattern explicitly:

- **Tool Wrapper**: Would the skill be stronger if it taught a library, domain, policy, or internal system through references?
- **Generator**: Would the skill benefit from templates, reusable output forms, or artifact generation?
- **Reviewer**: Does the skill need a rubric, checklist, scoring rule, or findings format?
- **Inversion**: Should the skill force clarifying questions or structured input gathering before acting?
- **Pipeline**: Should the skill enforce an ordered workflow with gates or checkpoints?

The pattern assessment may appear inside `Suggestions`, but it must show an explicit result for all five patterns, such as `applies`, `does not apply`, or `already present`. If a pattern applies, recommend it directly in the review rather than leaving the implication implicit.

## Another-AI Stability Checks

Ask these questions during review:
- Is the trigger description specific enough that an AI would load the skill at the right time?
- Are the first actions explicit after activation?
- Are references and assets named concretely?
- Are mandatory steps clearly marked?
- Are outputs constrained enough to be repeatable?
- Are there loopholes that let an AI skip key steps?
- Does the skill separate "when to use" from "how to do it" clearly enough for discovery and execution?

## Output Contract

Your final output must match `assets/review-template.md`.
Do not replace the requested sections with a different structure.
Write findings in natural prose. Explain impact directly instead of using the literal label `Why it matters:`.
