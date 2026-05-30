---
name: encode-tool-semantics
description: Capture tool and environment semantics for tool-enabled AI agents. Use before or during tasks involving shells, filesystems, browsers, IDEs, APIs, repositories, documents, spreadsheets, email, business apps, or platform-specific harnesses such as Codex, Claude Code, ChatGPT connectors, WorkBuddy, and CodeBuddy.
---

# Encode Tool Semantics

## Purpose

Before using an environment, encode how its tools actually behave. The goal is to prevent failures caused by wrong assumptions about side effects, permissions, state, paths, sessions, or verification.

## Tool Semantics Ledger

For any non-trivial tool workflow, maintain a compact ledger:

```text
Tool:
Available operations:
Read/write/network side effects:
Current state assumptions:
Common failure modes:
Verification signal:
Fallback:
```

Do not make the ledger verbose. Include only facts that change execution.

## Procedure

1. Inventory the environment.
   - Identify the workspace, active file or page, shell, browser, repository, account/session, and available connectors.
   - Identify whether the tool is read-only, local-write, networked, authenticated, or externally visible.

2. Bind paths and state.
   - Use exact paths, branch names, URLs, IDs, sheet names, document pages, or UI selectors.
   - Quote paths with spaces or non-ASCII characters.
   - Re-read current state after actions that may mutate files, pages, branches, or remote resources.

3. Prefer semantic operations.
   - Use APIs, parsers, tests, or platform-native tools instead of ad hoc text scraping when practical.
   - For spreadsheets, documents, PDFs, and code, prefer domain libraries or existing project tools.

4. Verify side effects.
   - After a write, check the actual target, not only the command exit code.
   - For UI/browser tasks, inspect visible state or screenshots when layout and interaction matter.
   - For remote systems, confirm identifiers, status, and final state before reporting completion.

5. Document reusable semantics.
   - If a repeated tool behavior caused success or failure, convert it into a concise rule for a future skill.
   - Record the rule as "when X, do Y, verify Z" rather than as a general warning.

## Platform Notes

- ChatGPT-style agents often depend on connectors and user-provided files; confirm what data is actually accessible.
- Codex-style agents share a local workspace; inspect before editing and use project-native commands.
- Claude Code and CodeBuddy-style agents commonly operate inside repositories; preserve user changes and validate with repo checks.
- WorkBuddy-style agents may act across business systems; distinguish draft preparation from externally visible action.

## Anti-Patterns

- Assuming a tool has the same behavior across platforms.
- Treating generated text as evidence when a tool output or file state can be checked.
- Continuing after an authenticated or external action boundary becomes unclear.
- Encoding vague rules such as "be careful with tools" instead of concrete tool semantics.
