# QuestionSetVersion

Aggregate: an immutable version of a [`QuestionSet`](question-set.md), created on publish. Sessions
snapshot it at start, and rankings bind to it. Editing mid-game or post-ranking cannot mutate
anything downstream.
