# Story quality reference

## INVEST (story must pass all six)

| Letter | Check | Failure smell |
| --- | --- | --- |
| **I**ndependent | Can be developed without depending on another story's order | "Requires X-12 finished first" |
| **N**egotiable | Details can be discussed; not a contract | Rigid spec copied from a vendor doc |
| **V**aluable | Delivers value to a user or the business | "Update internal config" with no user outcome |
| **E**stimable | Team can size it | Unknown scope, missing info, too broad |
| **S**mall | Fits comfortably in one sprint | Multi-week epic wearing a story costume |
| **T**estable | AC can verify it objectively | "Should work well", "be fast" |

Split recipes when size/testability fails: workflow steps · business rules ·
happy path / exceptions · data variations · operations (create/read/update) ·
interface permutations.

## Gherkin AC pattern

```gherkin
Scenario: <name>
  Given <preconditions with concrete data>
  When <the single action>
  Then <observable outcome>
  And <secondary outcome if any>
```

Rules: one scenario = one behavior; concrete values over placeholders ("email
`ana@x.com`" not "a valid email"); no UI steps in AC unless UI IS the feature;
negative scenarios are first-class (a "then it fails with X" scenario per
validation rule).

## Edge-case checklist (apply per story, keep what fits)

- Validation: empty, whitespace-only, too long, wrong type, boundary values
- Permissions: unauthenticated, wrong role, expired session
- State: already-done object, concurrent edit, retry after failure
- Data: first record (no history), large volume, unicode/emoji input
- Time: timezone, expiry, clock skew — only when the story touches time

## moSCoW flags

- **Must** — the story is worthless without it
- **Should** — valuable but the release survives a week without it
- **Could** — nice-to-have; cut first under pressure
- **Won't (this release)** — explicitly deferred; keep visible to kill scope creep
