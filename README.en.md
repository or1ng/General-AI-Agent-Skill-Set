# General AI Agent Skill Set

This directory contains five English skills for governing AI agents such as ChatGPT, Codex, Claude Code, WorkBuddy, and CodeBuddy.

The design follows an engineering interpretation of the two referenced papers: skills should be compact, extracted from real trajectories, evaluated by downstream utility, and optimized through bounded edits with regression checks. These five skills are deployment units, not a bundle that should always be injected together.

## Skill Map

| Skill | Purpose | Loading pattern |
| --- | --- | --- |
| `govern-agent-operation` | Runtime operating contract for assumptions, scope, safe action, verification, and delivery | Candidate default runtime skill |
| `encode-tool-semantics` | Encode tool behavior, platform constraints, side effects, and verification signals | Load for tool-enabled tasks |
| `extract-skills-from-experience` | Distill reusable skills from successful and failed agent trajectories | Use during offline skill production |
| `evaluate-skill-utility` | Evaluate skills with baselines, held-out cases, metrics, and negative-transfer checks | Use before accepting or comparing skills |
| `optimize-skill-artifacts` | Improve skill files with bounded add/delete/replace edits and validation gates | Use when iterating existing skills |

## Recommended Workflow

1. Use `govern-agent-operation` for ordinary agent execution.
2. Add `encode-tool-semantics` when the task involves shells, filesystems, browsers, APIs, repositories, documents, spreadsheets, or business systems.
3. Use `extract-skills-from-experience` after collecting real trajectories.
4. Use `evaluate-skill-utility` before accepting a generated or revised skill.
5. Use `optimize-skill-artifacts` to make small validated improvements to existing skills.

## Constraints

- Do not inject every skill into every task.
- Do not use textual plausibility as a substitute for utility evaluation.
- Do not put one-off examples, long explanations, or platform-specific clutter into general skills.
- If a skill causes regressions, narrow its trigger, remove overfit rules, or split it into a more targeted skill.
