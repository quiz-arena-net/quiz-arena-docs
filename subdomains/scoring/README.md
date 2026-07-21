# Scoring

Bounded context for the scoring subdomain (supporting). Pure consumer of resolution events, with no
coordination with gameplay internals.

## Aggregates

- [`Scoreboard`](models/scoreboard.md) (root, per session)

## Entities

- [`PlayerScore`](models/player-score.md)

## Value objects

- [`Points`](models/points.md)
- [`ScoreDelta`](models/score-delta.md)
- [`ScoringInput`](models/scoring-input.md)

## Policies

- [`BuzzOrderScoring`](models/buzz-order-scoring.md) (default)
- [`CompletionOrderScoring`](models/completion-order-scoring.md)
- Penalty rules for wrong answers (TBD)

## Key events

`PointsAwarded`, `PointsDeducted`, `LeaderboardUpdated`
