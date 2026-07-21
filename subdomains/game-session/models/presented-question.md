# PresentedQuestion

Entity inside the [`GameSession`](game-session.md) aggregate. A read-only snapshot of a question
from a `QuestionSetVersion`, taken at session start. Distinct from the editable `Question` in Quiz
Authoring and the answer key + format config in Judging. See the "Question means three things" note
in the [subdomain overview](../../README.md).
