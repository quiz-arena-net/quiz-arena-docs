# Identity & Presence

Bounded context for the identity & presence subdomain (generic). Buy or borrow. Don't innovate here.

## Aggregates

- [`PlayerAccount`](models/player-account.md) (root)
- [`Profile`](models/profile.md): largely a projection

## Value objects

- [`PlayerId`](models/player-id.md)
- [`Nickname`](models/nickname.md)
- [`ConnectionState`](models/connection-state.md)

## Key events

`PlayerRegistered`, `NicknameChanged`, `PlayerConnected`, `PlayerDisconnected`
