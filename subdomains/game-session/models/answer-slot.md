# AnswerSlot

Entity inside the [`GameSession`](game-session.md) aggregate: rank, holder, state. Per-slot track,
parallel to the question states `Arbitrating`/`Answering`:

`Claimed → AttemptRunning → Resolved (correct | incorrect | timed out) | Forfeited`

Slot ranks are contiguous 1..k and equal the arbitrated order (aggregate invariant).
