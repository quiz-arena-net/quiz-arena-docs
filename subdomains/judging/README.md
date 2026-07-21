# Judging

Bounded context for the answer judging subdomain (core). Runs a granted answer turn to a verdict.
Integration surface is deliberately tiny: `AnswerTurnGranted` in, `AnswerAttemptResolved` out.
Everything else is internal to the active policy.

*Open question (flagged): whether Judging warrants a separate context at all, or lives as pluggable
policies inside Game Session. Revisit when detailing `GameSession`. See ADR 0004.*

## Aggregates

- [`AnswerAttempt`](models/answer-attempt.md) (root): one player's attempt on one question.

## Entities

- [`CharacterStep`](models/character-step.md)

## Value objects

- [`AnswerKey`](models/answer-key.md)
- [`ChoiceSet`](models/choice-set.md)
- [`Choice`](models/choice.md)
- [`JudgingConfig`](models/judging-config.md)
- [`Verdict`](models/verdict.md)
- [`AttemptOutcome`](models/attempt-outcome.md)

## Policies (strategy implementations)

- [`ProgressiveChoiceJudge`](models/progressive-choice-judge.md) (default)
- [`FreeInputLlmJudge`](models/free-input-llm-judge.md)
- [`ExactMatchJudge`](models/exact-match-judge.md)

## Key events

- Published (cross-context): `AnswerAttemptStarted`, `AnswerAttemptResolved`
- Internal: `ChoiceSetPresented`, `ChoiceSelected`, `CharacterJudged`, `AttemptTimedOut`
