# InclusionPolicy

Value object on [`Quiz`](quiz.md). Whose quiz lists may include the quiz.

- `OwnerOnly`: only lists owned by the quiz's owner.
- `Anyone`: lists owned by anyone.

Sessions pose quizzes through quiz lists, so this governs who may redistribute the quiz through
their own lists, not who may play it. A quiz in a public list owned by its owner can be played by
anyone who can reach that list.

Checked when a quiz is added to a list and again when a session builds its lineup. An inclusion that
is no longer permitted stays in the list and is skipped.
