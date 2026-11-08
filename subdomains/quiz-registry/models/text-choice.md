# TextChoice

Value object, a [`ResponseMode`](response-mode.md). The player selects from predefined text answers.
Holds correct answers, wrong answers and a [`ChoiceRequirement`](choice-requirement.md).

## Invariants

- 1 to 6 answers across both sets, at least one correct.
- No answer is both correct and wrong.
- The wrong set may be empty, for example when every presented choice is intentionally correct.
- Each answer is 1 to 200 characters, single line, trimmed, NFC, no control characters.
