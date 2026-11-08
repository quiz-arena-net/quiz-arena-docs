# QuizList

Aggregate root. An ordered selection of quizzes: an identifier, an owner, a
[`QuizListTitle`](quiz-list-title.md), an optional
[`QuizListDescription`](quiz-list-description.md), a [`Visibility`](visibility.md), the current
[`QuizListEntries`](quiz-list-entries.md) version and a [`TagSet`](tag-set.md).

## Invariants

- A list refers to quizzes by identifier and does not own them. A quiz can appear in many lists,
  including lists owned by other users. Deleting a list does not delete its quizzes.
- The entries are versioned. Title, description, visibility and tags are not.
- Only the owner may edit.
- Two lists are equal when they have the same identifier.

## Operations

- `change_title`, `change_description`, `change_visibility`, `change_tags`.
- `add_quiz(quiz, position)`: fails on a duplicate, on the 101st quiz, or on a position past the
  end. Whether the quiz may be included is checked by the application through
  [`Quiz::includable_by`](quiz.md) before calling this.
- `remove_quiz`: fails when the quiz is not in the list.
- `reorder(order)`: fails unless `order` is a permutation of the current quizzes.
- `editable_by(user)`.
