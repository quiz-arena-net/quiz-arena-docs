# BuzzArbitrator

Domain service: RTT estimation + compensation + ordering of buzzes. The RTT estimate is the minimum
over a recent heartbeat window (see ADR 0002 and clock sync in
[`realtime-transport.md`](../../../engineering/integrations/realtime-transport.md)).
