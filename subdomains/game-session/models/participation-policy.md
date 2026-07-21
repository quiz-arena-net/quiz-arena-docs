# ParticipationPolicy

Policy: decides who participates in answering, at exactly three decision points. The
[`GameSession`](game-session.md) aggregate owns invariants. The policy chooses among *legal* options
only, so a policy bug can make a weird game, never a corrupt session (ADR 0003).

```rust
trait ParticipationPolicy {
    /// Slots to admit from this arbitration window's ordered buzzes.
    fn admit(&self, arbitrated: &[Buzz], claimed: &[SlotView]) -> usize;
    /// Player allowed to buzz right now? (lockouts after failed attempts, etc.)
    fn eligible(&self, p: &ParticipantView, q: &QuestionView) -> bool;
    /// After all active attempts resolve: keep going or wrap up?
    fn on_attempts_resolved(&self, outcomes: &[AttemptOutcome], q: &QuestionView) -> Directive;
}
enum Directive { ResumeReveal, CloseQuestion }
```

## Implementations

| | SequentialHayaoshi | ConcurrentBurst |
|---|---|---|
| Slots per window | 1 | up to remaining N |
| After wrong answer | lock player out, resume reveal | n/a (burst resolves as a whole) |
| Close condition | correct answer, or reveal done + deadline, or N attempts spent | burst resolved, or deadline |
| Information | later buzzers see more text and know prior attempts failed (strategic texture) | all claimants act at the same RevealMark |

Exclusive turn = SequentialHayaoshi with N = 1. Growth caution: if a new mode needs a fourth
decision point, suspect it is a different question *format* deserving its own machine, not another
policy.
