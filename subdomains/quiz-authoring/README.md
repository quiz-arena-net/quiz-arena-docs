# Quiz Authoring

Bounded context for the quiz authoring subdomain (supporting). Creation and editing. Publishing
produces immutable versions: the currency other contexts trade in.

## Aggregates

- [`QuestionSet`](models/question-set.md) (root)
- [`QuestionSetVersion`](models/question-set-version.md)

## Entities

- [`Question`](models/question.md)

## Value objects

- [`AnswerKey`](models/answer-key.md)
- [`QuestionText`](models/question-text.md)
- [`RevealScript`](models/reveal-script.md)
- [`SetVersionId`](models/set-version-id.md)
- [`Tag`](models/tag.md)
- [`Visibility`](models/visibility.md)

## Key events

`QuestionSetCreated`, `QuestionAdded`, `QuestionEdited`, `QuestionRemoved`, `QuestionSetPublished`
