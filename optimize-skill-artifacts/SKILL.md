---
name: optimize-skill-artifacts
description: Improve existing AI agent skill documents through bounded validated edits. Use when iterating a skill, applying rollout feedback, reducing skill bloat, fixing regressions, merging trajectory lessons, or running a SkillOpt-style add/delete/replace optimization loop.
---

# Optimize Skill Artifacts

## Principle

Treat the skill document as trainable external state. Make small edits, validate them, and keep only changes that improve downstream behavior.

## Edit Types

Use bounded edits instead of full rewrites:

- ADD: insert a missing procedure, boundary condition, verifier, or blacklist item.
- DELETE: remove generic, stale, duplicated, harmful, or over-specific text.
- REPLACE: tighten a vague rule into an executable rule or correct a wrong rule.

Default to 1-4 edits per iteration. Rewrite the whole skill only when the current structure is unusable and the user asked for a rebuild.

## Optimization Loop

1. Load the current skill and evidence.
   - Read the existing `SKILL.md`.
   - Collect failures, successes, evaluation results, user feedback, and rejected prior edits if available.

2. Propose candidate edits.
   - Tie each edit to a failure mechanism or measured opportunity.
   - State expected behavior change and risk.
   - Reject edits that only improve style or apparent completeness.

3. Apply a bounded patch.
   - Preserve trigger clarity in frontmatter.
   - Keep the body compact and procedural.
   - Avoid adding examples unless they prevent a known failure.

4. Validate.
   - Run the relevant evaluation, tests, examples, or manual checks.
   - Compare against the prior skill when possible.
   - Record negative-transfer cases separately.

5. Accept or reject.
   - Accept only verified improvement or a clearly justified safety correction.
   - Revert or revise harmful edits.
   - Keep rejected edit rationale as optimizer-side memory, not deployed skill text.

## Skill Compactness Rules

- Prefer dense instructions over long explanations.
- Move platform-specific detail into a separate targeted skill instead of bloating a general skill.
- Delete rules that do not change agent behavior.
- Keep deployment artifacts readable by a human in minutes.

## Edit Proposal Format

```text
Edit type:
Location:
Change:
Evidence:
Expected behavior:
Risk:
Verification:
Decision:
```

## Do Not Optimize Blindly

Do not accept edits based only on:

- The text sounding more polished.
- A stronger model preferring the new wording without utility criteria.
- One anecdotal failure when the rule would affect broad behavior.
- A benchmark-specific trick that will be loaded into unrelated domains.
