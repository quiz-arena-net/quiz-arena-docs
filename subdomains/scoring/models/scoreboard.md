# Scoreboard

Aggregate root, one per session. Holds [`PlayerScore`](player-score.md) entries.

## Invariants

- One entry per participant.
- Totals derived only from applied score deltas.
