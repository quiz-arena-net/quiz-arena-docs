# PromptText

Value object. The question text.

## Invariants

- 1 to 1000 characters in NFC.
- Not only whitespace. Multi-line: newline and tab are allowed, other control characters are not.
- Surrounding whitespace is kept.
