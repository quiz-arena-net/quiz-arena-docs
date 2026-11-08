# Quiz

Aggregate root. One question as its owner manages it: an identifier, an owner, an inclusion policy
and a state.

## State

- `Unpublished { draft }`: never published, only a [`DraftQuizContent`](draft-quiz-content.md)
  exists.
- `Published { content, draft }`: the latest [`QuizContent`](quiz-content.md) version and optionally
  a draft of the next one.

## Invariants

- The quiz keeps its identifier across versions. Statistics use the quiz identifier regardless of
  version.
- The inclusion policy and the draft are not versioned.
- Only the owner may edit: work on the draft, publish, change the inclusion policy, delete.
- Two quizzes are equal when they have the same identifier.

## Operations

- `edit_draft`: replaces the draft, or starts one.
- `discard_draft`: drops the draft of a published quiz. An unpublished quiz has nothing but its
  draft, so discarding it means deleting the quiz, which is a separate operation.
- `publish`: converts the draft into the next content version and consumes the draft. Fails when
  there is no draft or the draft is not ready (every violation is reported at once).
- `change_inclusion_policy`.
- `editable_by(user)`, `includable_by(list_owner)`: the questions the application asks before
  acting, see [`InclusionPolicy`](inclusion-policy.md).

## Ownership

The owner may change (transfer). The author recorded in the content's [`Source`](source.md) never
does.
