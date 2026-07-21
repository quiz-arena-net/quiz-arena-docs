# Ranking

Aggregate root, one per period/category. Holds [`RankingEntry`](ranking-entry.md)s.

## Invariants

- Entries ordered by ranking score.
- Only qualifying play events count (`RankingPolicy`, the integrity policy).
