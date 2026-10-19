---
name: ba-story-authoring
description: >
  Write or refine user stories with acceptance criteria: INVEST quality check,
  Given/When/Then scenarios, edge cases, and moSCoW scope flags. Use for
  "write a user story", "escribime una historia", "refine this story",
  "acceptance criteria", "criterios de aceptación", "AC para", "mejorar esta
  historia", "story grooming", "¿esta story está lista?". Output is Jira-ready
  text — posting to Jira requires explicit confirmation via /acli.
---

# ba-story-authoring

Turn an idea, ticket or conversation into a groomed user story: right-sized,
testable, with acceptance criteria a QA engineer can derive cases from.

## Inputs

| Input | Source |
| --- | --- |
| The idea | User description, existing Jira issue (via `/acli`, load it first), or meeting notes |
| Persona + value | Who benefits and why — ask ONLY if the story cannot be written meaningfully without it |
| Format | Gherkin AC (Given/When/Then) by default; bullet AC when the user prefers |

## Steps

1. **Clarify the goal.** One sentence: who, wants what, why. If two reasonable
   interpretations exist, present BOTH and ask — never pick silently.
2. **Draft the story.** `As a <persona>, I want <capability>, so that <value>`.
   Then check INVEST (reference in `references/story-quality.md`): if it fails
   size or testability, propose a split and say why.
3. **Write the AC.** Happy path first, then the edge cases that matter
   (validation, permissions, empty states, concurrency). Each AC is
   independently verifiable and free of implementation detail. Derive cases by
   technique (boundary values, state transitions) — not just the happy path.
4. **Flag scope.** moSCoW per requirement cluster; out-of-scope stated
   explicitly (what is NOT covered matters as much as what is).
5. **Deliver.** Jira-ready block: story title, description, AC, open questions,
   out-of-scope. Posting to Jira happens ONLY via `/acli` after the user
   confirms the exact text.

## Rules

- Stories describe WHAT and WHY, never HOW — no tech nouns unless the user
  asked for a technical story.
- Every AC must be testable by someone who was not in the conversation.
- Ambiguity is a finding, not something to paper over: list open questions
  instead of inventing answers.
- Never write to Jira from this skill; deliver text, post on confirmed request.
- Artifact language: Spanish by default (matches this team's Jira), English on
  request — user conversation always mirrored.
