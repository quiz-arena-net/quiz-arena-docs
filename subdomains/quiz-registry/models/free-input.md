# FreeInput

Value object, a [`ResponseMode`](response-mode.md). The player types an unrestricted answer. Holds
the expected answers used as the reference for judging.

## Invariants

- 1 to 20 expected answers, each 1 to 200 characters, single line, trimmed, NFC, no control
  characters.
