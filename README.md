# ralph-loop-skill

An iterative execution skill for CodeX/Codex that keeps work moving in short plan -> act -> check cycles until the task is actually complete.

Chinese summary:
`ralph-loop-skill` helps the agent avoid stopping at analysis, fake progress updates, repeated blind retries, and scope drift. It pushes each round to produce a real change, a verified result, or a clear reason to stop.

## What It Does

- Defines a finish line before major work begins
- Breaks progress into small meaningful loops
- Requires verification after each meaningful action
- Forces explicit continue, escalate, or stop decisions
- Reduces empty "still working" style progress claims

## Repository Layout

```text
.
|- README.md
`- ralph-loop-skill/
   |- SKILL.md
   |- agents/
   |  `- openai.yaml
   `- references/
      `- loop-patterns.md
```

## Install

Copy or symlink the `ralph-loop-skill/` folder into your local CodeX skills directory:

```powershell
New-Item -ItemType Directory -Force -Path "$HOME\\.codex\\skills" | Out-Null
Copy-Item -Recurse -LiteralPath ".\\ralph-loop-skill" -Destination "$HOME\\.codex\\skills\\ralph-loop-skill"
```

If you prefer a symlink:

```powershell
New-Item -ItemType SymbolicLink `
  -Path "$HOME\\.codex\\skills\\ralph-loop-skill" `
  -Target "D:\\path\\to\\this-repo\\ralph-loop-skill"
```

## When To Use It

Use this skill when you want CodeX/Codex to:

- keep iterating until the task is done
- work in repeated plan/act/check rounds
- continue after the first pass instead of stopping at analysis
- run fix/verify loops for code changes
- make progress visible and evidence-based

Typical prompts:

```text
Use ralph-loop-skill and keep iterating until this bug is fixed and verified.
Use ralph-loop-skill to work through this refactor step by step.
Use ralph-loop-skill and stop only when the requested outcome is complete or you hit a real blocker.
```

## Core Rule

The skill is built around one strict principle:

> Every loop must produce a real delta, a verified result, or a clear reason to stop.

That keeps the agent from:

- claiming progress without evidence
- retrying the same failed step without a new hypothesis
- editing before defining "done"
- continuing after the user request is already satisfied

## Included Files

- `ralph-loop-skill/SKILL.md`
  The main skill definition with workflow, stop conditions, anti-patterns, and delivery checks.
- `ralph-loop-skill/references/loop-patterns.md`
  Small templates for progress updates, escalation messages, and stop decisions.
- `ralph-loop-skill/agents/openai.yaml`
  UI metadata for environments that surface installed skills.

## Notes

- No license is included yet.
- The skill is intentionally compact so it is easier to audit and customize.
- If you want a more opinionated version, you can extend the reference file with domain-specific loop patterns.
