# JoinCode

Value object: a 6-char uppercase code from an unambiguous alphabet (no O/0, I/l). Format invariants
live in the VO. Uniqueness among active sessions is enforced at allocation by
[`JoinCodeAllocator`](join-code-allocator.md), not by the value.
