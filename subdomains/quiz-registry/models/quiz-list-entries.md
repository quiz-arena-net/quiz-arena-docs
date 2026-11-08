# QuizListEntries

Entity inside [`QuizList`](quiz-list.md). One version of the ordered quizzes in a list, identified
by its own `QuizListEntriesId`. Every change to the quizzes (add, remove, reorder) creates a new
version.

## Invariants

- At most 100 quizzes.
- No quiz twice.
- May be empty. May refer to quizzes that no longer exist.
- Two versions are equal when they have the same identifier.

Rehydration from storage rechecks these invariants.
