# Research Facility

This repo is a research facility. Each research topic lives in its own directory under `research/`.

## How Research Works

When the user requests a research session on a topic:

1. **Create the topic directory** at `research/<topic-slug>/` if it doesn't exist.
2. **Enter plan mode** and design a multi-phase research plan before doing any work.
3. **Spawn a single Agent** (subagent_type: general-purpose) that carries out the entire research plan autonomously.
4. **The orchestrator (this session) does not do research itself.** It only:
   - Creates the topic directory
   - Designs the plan
   - Launches the Agent with a comprehensive prompt
   - Reports results back to the user

## Research Directory Structure

```
research/
  <topic-slug>/
    plan.md          — the multi-phase research plan
    findings.md      — consolidated findings
    phase-N/         — per-phase working files, logs, artifacts
    sources.md       — references and sources used
```

## Multi-Phase Plan Format

Every research session follows this structure (see `templates/plan-template.md`):

- **Phase 1: Scoping** — Define research questions, boundaries, success criteria
- **Phase 2: Discovery** — Broad search, source gathering, landscape mapping
- **Phase 3: Deep Analysis** — Focused investigation of key areas
- **Phase 4: Synthesis** — Cross-reference findings, identify patterns, form conclusions
- **Phase 5: Output** — Write up findings.md, sources.md, and any artifacts

Phases can be added/removed/modified based on the topic. The plan is saved to `research/<topic>/plan.md` before the Agent is launched.

## Agent Prompt Template

When launching the research Agent, include:

1. The full research plan
2. The working directory path (`research/<topic-slug>/`)
3. Instructions to log work into phase subdirectories
4. Instructions to produce `findings.md` and `sources.md` at the end
5. Permission to use all tools: Bash, Read, Write, Edit, WebFetch, WebSearch, Glob, Grep, etc.

## Rules

- ALL tool calls are pre-approved in `.claude/settings.json`.
- The orchestrator session stays thin — it plans and delegates, nothing else.
- Each Agent works autonomously through the full plan without needing orchestrator intervention.
- If the user asks to continue or extend a research topic, read the existing plan/findings and spawn a new Agent for the next phase.

## Directive: "Research autonomously"

When the user's prompt contains **"Research autonomously"**, run the whole
methodology above end-to-end with zero further questions:

1. Slugify the topic → `research/<topic-slug>/`.
2. Write `plan.md` from `templates/plan-template.md` (all 5 phases, topic-adapted).
   Skip plan mode and skip approval — the directive IS the approval.
3. Launch ONE Agent (`subagent_type: general-purpose`) with the full plan, the
   working dir, phase-logging instructions, and all-tools permission.
4. Report back in one line when it finishes.

Never do the research in the orchestrator session.

## Communication Rule (HARD)

Replies must not exceed the user's own word count by more than 10 words.
5-word question → ~5-word answer. This is a brainstorming facility, not an
essay pitch. One-liners by default. Non-negotiable.
