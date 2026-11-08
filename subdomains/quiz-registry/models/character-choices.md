# CharacterChoices

Value object, a [`ResponseMode`](response-mode.md). The player builds the answer one position at a
time by picking from candidate [`Character`](character.md)s. The order of positions is the order of
characters in the answer.

Each position is a `CharacterChoice`: one correct character and a set of wrong ones.

## Invariants

- 1 to 50 positions.
- Per position: exactly one correct character and 1 to 9 wrong ones, the correct one not among them.

Converting a draft stops at the first position that is missing a correct or a wrong character, or
whose correct character is also listed as wrong, and reports the position.
