# Research Facility

Intent-based research powered by Claude Code. Each topic gets its own directory, a multi-phase plan, and a fully autonomous research Agent.

## Usage

Start a Claude Code session in this repo and request a research topic:

```
"Research <topic>"
```

Claude Code will:
1. Create `research/<topic-slug>/`
2. Design a multi-phase research plan
3. Spawn an autonomous Agent to execute the full plan
4. Report back with findings

## Structure

```
research/              — all research topics
  <topic>/
    plan.md            — multi-phase plan
    findings.md        — final output
    sources.md         — references
    phase-N/           — per-phase working files
templates/             — plan templates
CLAUDE.md              — orchestrator instructions
.claude/settings.json  — all permissions pre-approved
```

## Principles

- **Orchestrator stays thin** — plans and delegates, doesn't do research itself
- **Agent does all work** — autonomous, multi-phase, tool-unrestricted
- **Everything is logged** — plans, phase artifacts, sources, findings
