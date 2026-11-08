# Tag

Value object. A word used to classify or discover quizzes and quiz lists.

## Invariants

- 1 to 32 characters in NFC, single line, trimmed, no control characters.

## Open point

Case and width are not folded: `Tokyo`, `tokyo` and fullwidth `Ｔｏｋｙｏ` are three tags.
