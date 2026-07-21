# JoinCodeAllocator

Domain service: issues [`JoinCode`](join-code.md)s unique among *active* sessions. Codes are
recyclable after a session closes. Implemented as a central registry providing global uniqueness and
code → region → node routing (ADR 0008).
