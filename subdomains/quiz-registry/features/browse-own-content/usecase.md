# Browse own content

Actor: a user looking at what they own.

## List my quizzes

- Input: page (offset and limit, limit at most 50 **(assumed)**).
- Steps: `QuizRepository::find_by_owner(caller, page)`.
- Returns the aggregates. Presentation shows identifier, state (unpublished, published, published
  with a draft), prompt text of the latest version or draft, tags, inclusion policy.
- Order: newest first by identifier, which is time-ordered (UUIDv7) **(assumed)**. There is no
  `updated_at` in the model.

## List my quiz lists

- Same shape: `QuizListRepository::find_by_owner(caller, page)`.

## Notes

- These read through the aggregate repositories (no separate read model). If a listing turns out to
  be slow, it moves to a query service that bypasses the domain, see the CQRS discussion in the
  context README.
- Search and discovery of other users' content is Community & Discovery, not this context.

## Repository needs

`QuizRepository::find_by_owner`, `QuizListRepository::find_by_owner`, both paginated.
