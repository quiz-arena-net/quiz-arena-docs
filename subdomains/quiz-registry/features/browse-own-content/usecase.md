# Browse own content

Actor: a user looking at what they own.

## List my quizzes

- Input: the order (`QuizOrder`: most recently created first, or most recently changed first) and a
  page (`Page<50>`: offset and limit, limit 1 to 50).
- Steps: `QuizRepository::find_by_owner(caller, order, page)`.
- Returns the aggregates. Presentation shows identifier, state (unpublished, published, published
  with a draft), prompt text of the latest version or draft, tags, inclusion policy, created and
  changed times.
- Identifiers are never used for ordering. Time comes from `created_at` and `updated_at`.

## List my quiz lists

- Same shape: `QuizListRepository::find_by_owner(caller, order, page)` with `QuizListOrder`.

## Notes

- These read through the aggregate repositories (no separate read model). If a listing turns out to
  be slow, it moves to a query service that bypasses the domain, see the CQRS discussion in the
  context README.
- Search and discovery of other users' content is Community & Discovery, not this context.

## Repository needs

`QuizRepository::find_by_owner`, `QuizListRepository::find_by_owner`, both ordered and paginated.
