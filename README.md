# agentic-ba-harness

Agent console for **Business Analyst workflows**: user stories with acceptance
criteria, business process mapping (as-is / to-be), and Jira access via the
Atlassian CLI.

## What's inside

```
.opencode/skills/
  ba-story-authoring/        User stories + Gherkin AC, INVEST check, moSCoW scope
  ba-process-mapping/        As-is / to-be process maps (mermaid) + handoff + gap analysis
  acli/                      Atlassian CLI skill (Jira Cloud)
  git-flow-master/           Git operator skill
  caveman/                   Terse voice skill (vendored from github.com/JuliusBrussee/caveman, Apache-2.0)
opencode.jsonc               OpenCode MCP config (engram + tavily)
.env.example                 Credential template
AGENTS.md                    Agent operating rules
reports/                     Saved artifacts (process maps, story drafts) — only on request
```

## Setup

1. `cp .env.example .env` and fill in your credentials (`ATLASSIAN_*`,
   `TAVILY_API_KEY`).
2. Make sure `engram` is on your PATH and `TAVILY_API_KEY` is set before
   starting the agent session — MCP env vars are read at spawn time.
3. Open the repo in your agent and invoke skills by name
   (`/ba-story-authoring`, `/ba-process-mapping`, `/acli`).

## Typical flows

```text
"write a user story for password reset"     → /ba-story-authoring → Jira-ready text
"map our refund process today"              → /ba-process-mapping → mermaid map + handoffs
"what changes if we add auto-approval"      → /ba-process-mapping (as-is + to-be) → gap table
"post that story to Jira BK-123"            → confirmed plan → /acli (the only write path)
```

## Rules of the road

- Credentials always from `.env`; never hardcoded.
- MCP or auth failure = STOP and name the missing env var; no workarounds.
- Jira writes only via `/acli` with explicit confirmation of the exact text
  or action — skills produce artifacts, they never post on their own.
- As-is maps model what happens, including pain — smoothing it over hides the
  analysis.
- No AI attribution in commits; confirm before push.
- Caveman voice is the default for conversation; code/commits/artifacts stay
  normal English or Spanish — that boundary is built into the skill.

## Upstream attribution

- `caveman` skill — © 2026 Julius Brussee, Apache-2.0. See
  `.opencode/skills/caveman/LICENSE-APACHE-2.0` and `NOTICE` in this directory.
- `acli`, `git-flow-master` — copied from the project QA boilerplate.
