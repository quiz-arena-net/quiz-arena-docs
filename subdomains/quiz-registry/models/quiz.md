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

## Time

`created_at` is set once by `new`. `updated_at` is set by `new` and by every operation that changes
the quiz. Both come from the caller as the `now` argument: the domain never reads the clock, and a
use case stamps one time on everything it touches. A rejected operation leaves `updated_at` alone.

## Operations

- `edit_draft`: replaces the draft, or starts one.
- `discard_draft`: drops the draft of a published quiz. An unpublished quiz has nothing but its
  draft, so discarding it means deleting the quiz, which is a separate operation.
- `publish`: converts the draft into the next content version and consumes the draft. Fails when
  there is no draft or the draft is not ready (every violation is reported at once).
- `change_inclusion_policy`.
- `is_editable_by(user)`: the authorization question the application asks before acting.
- `is_published()`, `is_includable_by(list_owner)`: whether a list owned by `list_owner` may include
  the quiz. True only for a published quiz, and then for the owner always and for anyone else under
  `InclusionPolicy::Anyone`, see [`InclusionPolicy`](inclusion-policy.md).
  [`QuizList::add_quiz`](quiz-list.md) applies it. Sessions apply it again when resolving a list.

## Ownership

The owner may change (transfer). The author recorded in the content's [`Source`](source.md) never
does.
