---
name: evaluate-skill-utility
description: Evaluate whether an AI agent skill improves downstream behavior. Use when reviewing, selecting, accepting, rejecting, comparing, or regression-testing skills with baselines, held-out tasks, task metrics, user feedback, or negative-transfer checks.
---

# Evaluate Skill Utility

## Principle

Judge a skill by measured downstream behavior, not by whether the text sounds clear, complete, or professional.

## Evaluation Workflow

1. Define the baseline.
   - Run or inspect the agent behavior without the skill.
   - Record task success, failure mode, time/cost if relevant, and output quality.

2. Define the skill condition.
   - Run the same or comparable tasks with the skill injected.
   - Keep model, tools, harness, data, and scoring method fixed when possible.

3. Use held-out checks.
   - Avoid accepting a skill only because it explains the trajectory it was extracted from.
   - Test on new tasks, unseen files, alternate examples, or a regression suite.

4. Measure utility.
   - Use exact metrics when available: pass/fail, test count, score, accuracy, lint, render result, user acceptance, or task completion.
   - For qualitative tasks, use a rubric tied to the user's outcome, not generic writing quality.

5. Check negative transfer.
   - Look for tasks where the skill makes behavior worse.
   - Identify whether the regression came from over-specific rules, wrong tool semantics, excessive caution, format interference, or strategy mismatch.

6. Decide.
   - Accept the skill only when it improves the target behavior or removes a clear risk without causing meaningful regressions.
   - Reject, narrow, or revise the skill when gains are unmeasured, mixed, or based only on textual plausibility.

## Pairwise Skill Review

When comparing two skills:

- Prefer the skill with better measured utility.
- If utility data is unavailable, prefer the skill that encodes concrete failure mechanisms, actionable steps, and specific risk boundaries.
- Do not prefer a skill merely because it is longer, more polished, more general, or more confident.

## Evaluation Report

Use this compact report:

```text
Baseline:
Skill condition:
Tasks or cases:
Metric:
Result:
Negative transfer observed:
Decision:
Next edit:
```

## Common Failure Modes

- Evaluating only on the examples used to create the skill.
- Using an LLM judge without validated criteria.
- Treating no observed failure as proof of improvement.
- Ignoring weaker models or different harnesses that may consume the skill differently.
- Accepting broad advice that does not change agent behavior.
