# Game Session

Bounded context for the gameplay subdomain (core). Orchestrates a live game: rounds, buzzing, slot
management, turn granting.

## Aggregates

- [`GameSession`](models/game-session.md) (root): the invariant keeper. Covered in depth there:
  state machine, invariants, buzz arbitration, reveal timeline, runtime shape.
- [`RuleSet`](models/rule-set.md): versioned bundle of policy configuration.

## Entities (inside GameSession)

- [`Round`](models/round.md)
- [`PresentedQuestion`](models/presented-question.md)
- [`AnswerSlot`](models/answer-slot.md)
- [`Participant`](models/participant.md)

## Value objects

- [`JoinCode`](models/join-code.md)
- [`SessionState`](models/session-state.md)
- [`SlotRank`](models/slot-rank.md)
- [`BuzzTimestamp`](models/buzz-timestamp.md)
- [`CompensatedBuzzTime`](models/compensated-buzz-time.md)
- [`RuleSetSnapshot`](models/rule-set-snapshot.md)
- [`RevealMark`](models/reveal-mark.md)
- [`RevealSegment`](models/reveal-segment.md)

## Policies and domain services

- [`ArbitrationPolicy`](models/arbitration-policy.md)
- [`ParticipationPolicy`](models/participation-policy.md)
- [`BuzzArbitrator`](models/buzz-arbitrator.md) (domain service)
- [`JoinCodeAllocator`](models/join-code-allocator.md) (domain service)

## Key events

`GameSessionOpened`, `PlayerJoined`, `GameStarted`, `QuestionPresented`, `RevealStarted`,
`RevealPaused`, `RevealResumed`, `PlayerBuzzed`, `BuzzArbitrated`, `AnswerSlotClaimed`,
`AnswerTurnGranted`, `QuestionClosed`, `RoundEnded`, `GameEnded`, `ResultsPublished`
