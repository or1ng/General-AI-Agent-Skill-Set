---
name: extract-skills-from-experience
description: Distill compact procedural skills from real agent trajectories. Use when given execution logs, transcripts, rollouts, benchmark traces, project memories, failed runs, successful runs, or user feedback and asked to create or update reusable AI agent skills from experience.
---

# Extract Skills From Experience

## Principle

Extract skills from observed behavior, not from plausible advice. A useful skill explains why agents fail, what action prevents the failure, and how to verify success.

## Required Inputs

Use as many of these as are available:

- Task prompt and intended outcome.
- Environment and tool context.
- Trajectory: messages, tool calls, observations, file changes, UI state, or logs.
- Outcome: success, failure, score, user correction, or test result.
- Existing skill text, if updating a skill.

If outcome evidence is missing, mark conclusions as hypotheses and do not present them as validated rules.

## Extraction Workflow

1. Separate successes and failures.
   - Successes reveal procedures worth preserving.
   - Failures reveal missing rules, unsafe shortcuts, and tool misunderstandings.
   - Pure failure pools are weak evidence; look for at least one successful or corrected trajectory when possible.

2. Encode failure mechanisms.
   - Name why the agent failed, not just what went wrong.
   - Classify failures as task misunderstanding, missing context, wrong tool semantics, unsupported environment assumption, weak verification, formatting violation, over-broad action, or unsafe action.

3. Extract actionable rules.
   - Write step-level procedures tied to domain objects, files, tools, APIs, UI elements, or evaluation criteria.
   - Use "when condition, do action, verify signal" form.
   - Prefer one reusable rule over a story about one case.

4. Add risk boundaries.
   - Include blacklisted actions only when the trajectory shows realistic harm or repeated error.
   - Include edge cases and strategy-switch conditions only when they change behavior.

5. Synthesize the skill.
   - Keep the deployed skill compact, ideally under 2,000 tokens unless the domain demands more.
   - Put trigger conditions in the frontmatter description.
   - Keep the body procedural and imperative.
   - Remove examples that are too instance-specific to guide future tasks.

## Utility-Oriented Rubric

Prioritize rules with these properties:

- Failure mechanism encoding: the rule explains why the model fails.
- Actionable specificity: the rule gives concrete steps and references the relevant tools or objects.
- High-risk action blacklist: the rule prevents specific harmful behaviors.
- Environment semantics: the rule captures how tools actually behave.
- Boundary coverage: the rule says when to stop, switch, or ask.

Do not prioritize surface polish, long explanations, generic principles, or formatting style unless they affect utility.

## Output Shape

When producing a candidate skill, include:

```text
Skill name:
Trigger description:
Core workflow:
Failure mechanisms covered:
High-risk blacklist:
Verification method:
Evidence source:
```

If the user asks for files, create a standard skill folder with `SKILL.md` and optional resources only when they directly support execution.
