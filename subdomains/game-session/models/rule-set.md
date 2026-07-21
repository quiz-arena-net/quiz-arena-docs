# RuleSet

Aggregate. Versioned bundle of policy configuration: arbitration cap, judging policy + params,
participation N, scoring mode. Sessions bind to an immutable RuleSet version at `GameStarted` (see
invariant 6 in [`GameSession`](game-session.md)). Could later move to its own tiny "Game
Configuration" context. Keep it here until it grows.
