# AnswerAttempt

Aggregate root: one player's attempt on one question.

## Invariants

- Belongs to exactly one granted turn.
- Resolves exactly once (completed / failed / timed out).
- Progressive policy steps ([`CharacterStep`](character-step.md)) advance strictly in character
  order.
