# ArbitrationPolicy

Policy: capped latency compensation for buzz ordering. cap = 0 ⇒ raw server-receive order. The cap
is simultaneously the fairness bound and the reordering window. See arbitration in
[`GameSession`](game-session.md) and ADR 0002.
