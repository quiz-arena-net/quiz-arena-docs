# Curate a quiz list

Actor: a user working on their own list. Aggregate: [`QuizList`](../../models/quiz-list.md).

## Create a list

- Input: title, optional description, visibility, tags, and optionally the quizzes to start with.
- Steps: `QuizList::new(caller, title, description, visibility, tags)` creates the list without
  quizzes. Each initial quiz then goes through "Add a quiz" below, in order.
  `QuizListRepository::add`.
- No server-side defaults. Visibility is required input.
- Rejected when: a text field fails to parse, more than 10 tags, or any initial quiz is rejected by
  "Add a quiz".

## Change title, description, visibility or tags

- Steps: `find_by_id`, `is_editable_by`, the matching `change_*`, `update`.
- These fields are not versioned. The entries version is untouched.

## Add a quiz

- Steps: `QuizListRepository::find_by_id`, `is_editable_by`, `QuizRepository::find_by_id(quiz_id)`,
  `QuizList::add_quiz(&quiz, position)`, `update`.
- `add_quiz` enforces the rule: the quiz must be published (a draft has nothing to play) and must
  allow inclusion in a list owned by this list's owner (`Quiz::is_includable_by`). The application
  only loads the quiz and passes it in.
- Rejected when: the quiz is not found, unpublished, not includable, already in the list, the list
  is full, or the position is past the end.
- Outcome: a new entries version.

## Remove a quiz, reorder

- Steps: `find_by_id`, `is_editable_by`, `remove_quiz` or `reorder`, `update`.
- Rejected when: the quiz is not in the list, or the order is not a permutation of the current
  quizzes.
- Outcome: a new entries version.

## Delete a list

- Steps: `find_by_id`, `is_editable_by`, `QuizListRepository::remove(id)`.
- Hard delete. Quizzes are untouched. Running sessions keep the entries version they started with.

## Repository needs

`QuizListRepository::find_by_id`, `add`, `update`, `remove`. `QuizRepository::find_by_id` for the
inclusion check.
