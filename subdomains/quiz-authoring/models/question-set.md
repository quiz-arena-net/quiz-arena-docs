# QuestionSet

Aggregate root: a mutable draft holding [`Question`](question.md)s, with a pointer to the latest
published [`QuestionSetVersion`](question-set-version.md).

## Invariants

- A set has ≥ 1 question to publish.
- Every question has a valid answer key for at least one judging policy.
