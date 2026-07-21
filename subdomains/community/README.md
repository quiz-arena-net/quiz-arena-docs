# Community & Discovery

Bounded context for the content community subdomain (core). The content flywheel: sharing,
popularity, rankings, creator recognition. Moderation (supporting, deferred) lives inside this
context for now.

## Aggregates

- [`SharedSetListing`](models/shared-set-listing.md) (root)
- [`Ranking`](models/ranking.md) (root, per period/category)
- [`CreatorReputation`](models/creator-reputation.md) (root, per creator)
- [`Group`](models/group.md) (root)

## Entities

- [`RankingEntry`](models/ranking-entry.md)
- [`Badge`](models/badge.md)

## Value objects

- [`PopularitySignal`](models/popularity-signal.md)
- [`LikeCount`](models/like-count.md)
- [`RankingPeriod`](models/ranking-period.md)
- [`RankingScore`](models/ranking-score.md)
- [`BadgeCriteria`](models/badge-criteria.md)

## Policies

- [`RankingPolicy`](models/ranking-policy.md)
- [`BadgeAwardPolicy`](models/badge-award-policy.md)

## Key events

`SetSharedToCommunity`, `SetLiked`, `PlayRecorded` (consumed from Game Session),
`RankingRecalculated`, `BadgeAwarded`, `SetReported`, `SetDelisted`, `GroupCreated`,
`GroupMemberJoined`
