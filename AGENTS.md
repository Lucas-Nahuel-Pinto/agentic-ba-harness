# AGENTS.md — agentic-ba-harness

BA console: user stories with acceptance criteria, business process mapping,
and Jira access via the Atlassian CLI.

## Critical rules

1. **CREDENTIALS**: ALWAYS read from `.env` (see `.env.example`). NEVER hardcode or guess secrets. Example keys: `ATLASSIAN_API_TOKEN`, `TAVILY_API_KEY`.
2. **MCP / AUTH FAILURE = STOP IMMEDIATELY**: if an MCP fails auth or an env var is missing (`.mcp.json` uses `${VAR}` for Claude Code; `opencode.jsonc` uses `{env:VAR}` for OpenCode — OpenCode substitutes empty silently, so a 401/403 is the signal), do NOT work around it. STOP, name the exact env variable, point at `.env` / `.env.example`, and ask the user to fix `.env` + restart the agent session (env is cached at MCP spawn time).
3. **JIRA WRITES = CONFIRMATION REQUIRED**: story drafts, process maps and gap analyses are ARTIFACTS produced by skills. Posting anything to Jira goes through `/acli` and only after the user confirms the exact text or action. No silent writes, no bulk edits.
4. **AMBIGUITY IS A FINDING**: when a requirement admits two interpretations, present both and ask. Never invent intent to fill a gap — list open questions instead.
5. **GIT / PR WORK**: follow `.claude/skills/git-flow-master/` conventions if git work arises — semantic commit prefixes, no AI attribution, confirm before push.
6. **DEFAULT VOICE**: caveman mode is the default conversational register (`.claude/skills/caveman/`). Code, commits, Jira comments, and artifact files are ALWAYS written in normal English (or Spanish when the user asks) — that boundary is built into the skill.

## Skills

| Skill | Purpose |
|---|---|
| `.claude/skills/ba-story-authoring/` | User stories + Gherkin AC, INVEST check, moSCoW scope flags |
| `.claude/skills/ba-process-mapping/` | As-is / to-be process maps (mermaid), handoff tables, gap analysis |
| `.claude/skills/acli/` | Atlassian CLI for Jira Cloud issues, comments, transitions |
| `.claude/skills/git-flow-master/` | End-to-end git operator (branch, commit, PR, conflicts) |
| `.claude/skills/caveman/` | Terse conversational voice (vendored, Apache-2.0) |

## MCPs

| MCP | Use |
|---|---|
| `engram` | Persistent memory across sessions |
| `tavily` | Web search (domain research, troubleshooting) |

## Language

- Conversation: mirror the user's language.
- Artifacts (Jira text, maps, files): Spanish by default (this team's Jira),
  English on request. Always confirm the language for anything posted to Jira.
