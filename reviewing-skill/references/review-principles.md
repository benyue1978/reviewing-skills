# Review Principles

Use these principles when reviewing a skill.

## 1. Match The Pattern To The Job

Review whether the skill uses the right structural pattern, not just whether the prose sounds good.

Check all five patterns:

- **Tool Wrapper**
Use when the skill mainly teaches conventions for a library, framework, domain, policy, or internal system. Good signs: focused domain, strong references, concrete rules.
Weak signs: vague "best practices", no domain reference, generic advice pretending to be expertise.

- **Generator**
Use when the skill must create repeatable structured output. Good signs: templates, placeholders, stable sections, examples.
Weak signs: free-form output even though the user expects a standard artifact.

- **Reviewer**
Use when the skill evaluates something against a rubric or checklist. Good signs: severity model, criteria, citation rules, stable findings format.
Weak signs: "review this" without a rubric, inconsistent severity, no evidence expectations.

- **Inversion**
Use when the agent should ask questions before acting. Good signs: required questions, one-at-a-time flow, explicit approval gates.
Weak signs: hidden assumptions, premature action, underspecified inputs.

- **Pipeline**
Use when quality depends on a strict order of operations. Good signs: ordered steps, mandatory checkpoints, stop conditions, output gates.
Weak signs: important steps implied but not enforced.

Recommend any missing pattern that would materially improve the skill.

## 2. Optimize For Discovery

The skill description is the trigger surface.

Check whether the description:
- starts with a concrete "Use when..." trigger
- names realistic user intents and symptoms
- avoids vague wording like "helps with" or "best practices"
- avoids summarizing the full workflow so heavily that the AI may skip the body

Poor discovery leads to non-use or incorrect use.

## 3. Keep Instructions Lean, Push Detail Down

Check whether the skill uses progressive disclosure well:
- `SKILL.md` should hold activation logic, workflow, and critical constraints
- `references/` should hold heavier rubrics, conventions, and detailed guidance
- `assets/` should hold templates and reusable output shapes
- `scripts/` are optional and should exist only when execution adds real reliability

Flag skills that bury critical steps in reference files with no pointer from `SKILL.md`.

## 4. Make The Next Action Obvious

After activation, another AI should know exactly what to do next.

Check whether the skill clearly answers:
- what to read first
- what to read only if needed
- what to produce
- in what order
- when to stop or ask for confirmation

If the next action is ambiguous, the skill is unstable.

## 5. Close Loopholes

Review the skill for rationalizations an AI could use to skip important work.

Examples:
- mandatory steps described as optional
- soft verbs like "consider" where the behavior must be required
- no enforcement of failure checks, approval gates, or template use
- no distinction between findings and suggestions

If a step is necessary, the wording should be hard to misread.

## 6. Constrain Output Enough To Be Reusable

Good skills do not only say what to think about. They also constrain what to return.

Check for:
- a stable output structure
- expectations for severity or prioritization
- evidence requirements
- explicit requests to cite files and lines when reviewing artifacts

If output quality matters and no template exists, consider recommending the Generator pattern.

## 7. Review For Portability

Since the target may be used across agents, check for:
- portable directory layout and naming
- minimal dependence on one agent's private tool names or modes
- explicit fallback behavior when referenced files do not exist
- language that remains valid outside a single platform

If the skill is intentionally platform-specific, it should say so plainly.

### Packaging Sanity Check

When the target claims to be a packaged skill, sanity-check:
- whether `SKILL.md` exists
- whether frontmatter includes `name` and `description`
- whether `references/`, `assets/`, and `scripts/` are used only when they add value
- whether `SKILL.md` points to any required reference or template files
- whether the package layout matches the intended portability claim

If the target is not packaged, do not treat missing package files as a defect by default. Instead, note that packaging checks were limited because the review target was a document rather than an official skill package.

## 8. Simulate Another AI Using The Skill

Perform a mental dry run:

1. The AI sees only the name and description.
2. The AI decides whether to load the skill.
3. The AI reads `SKILL.md`.
4. The AI chooses what resource to load next.
5. The AI performs the steps.
6. The AI formats the output.

At each step, look for ambiguity, missing guidance, conflicting instructions, and incentives to skip work.

## 9. Prefer Actionable Findings

Findings should point to a fixable issue.

Strong finding:
- identifies the exact weakness
- explains behavioral impact
- cites where it occurs
- suggests the class of fix

Weak finding:
- generic praise or generic dislike
- no user impact
- no location
- no explanation of why it matters

## 10. Distinguish Findings From Suggestions

- **Findings** are concrete current problems.
- **Bottom line** is what must be fixed before relying on the skill.
- **Suggestions** are optional improvements or pattern recommendations beyond must-fix issues.

Do not hide must-fix problems inside the suggestions section.
