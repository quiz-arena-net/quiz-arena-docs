# DraftQuizContent

Value object. A [`QuizContent`](quiz-content.md) that may still be incomplete.

Prompt text, canonical answer and response mode may be missing. The response mode, when present, is
a draft response mode and may itself be incomplete. Language, tags, source and usage terms are
always present.

## Invariants

- Every size limit of the published form holds: tags are a [`TagSet`](tag-set.md), the draft
  response modes keep their limits.
- Any text present is a valid text value. A draft holds either a complete value or none.
