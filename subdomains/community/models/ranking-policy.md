# RankingPolicy

Policy: decides which `GameCompleted` events qualify for rankings (distinct players, minimum lobby
size, decay). v1 may be like-count based. Likes and plays are both farmable (self-plays, bot
lobbies), so this is the ranking-integrity hotspot (open question 1 in the
[subdomain overview](../../README.md)).
