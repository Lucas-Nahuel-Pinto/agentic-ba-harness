---
name: ba-process-mapping
description: >
  Map a business process as-is or design it to-be: step sequences, decision
  points, handoffs between roles/systems, and gap analysis between current
  and future state. Use for "map the process", "mapeá el proceso", "cómo
  funciona hoy", "proceso actual", "diseñar el flujo futuro", "to-be flow",
  "gap entre proceso actual y nuevo", "BPMN", "flujo de negocio". Output is
  a mermaid diagram + step table in markdown.
---

# ba-process-mapping

Capture how a process runs today (as-is) or how it should run after a change
(to-be), as a mermaid flowchart plus a handoff table. The diagram is the
argument — prose only explains what the diagram cannot.

## Inputs

| Input | Source |
| --- | --- |
| The process | User description, interview notes, or observed tickets via `/acli` |
| State | as-is (default when "how does it work"), to-be (default when "how should it work"), or both for gap analysis |
| Scope boundaries | Where does the process start (trigger) and end (outcome) — ask if the user's description overruns |

## Steps

1. **Set the boundaries.** Trigger in, outcome out. Anything outside belongs
   to another map; say what was cut.
2. **Enumerate the steps.** For each: actor (role or system), action, and
   decision points with their branches. Loops and rework paths are steps too —
   usually the most valuable ones.
3. **Diagram it.** Mermaid `flowchart TD`: swimlanes by actor where helpful,
   decisions as diamonds, systems as distinct node shapes. Keep under ~20
   nodes; more means the map needs decomposition — propose the split.
4. **Handoff table.** Steps where the work changes hands (role→role,
   system→human) get a table row: from · to · artifact passed · wait state.
   Handoffs are where processes actually break — never skip this.
5. **Gap analysis (to-be vs as-is, when both exist).** Per change: step added
   / removed / modified, plus the WHY in one line each. No unexplained deltas.
6. **Deliver.** Markdown file with the mermaid diagram + tables; save under
   `reports/` only if the user asks, chat output by default.

## Rules

- One map = one process; nested subprocesses get their own map + reference.
- Model what HAPPENS, not what should happen (as-is discipline: pain points
  and workarounds are data, not noise to smooth over).
- Actor names are roles ("Support Agent"), never people.
- Mermaid must render: validate syntax mentally (no reserved words unquoted).
- Language: Spanish for the user's artifact by default, English on request.
