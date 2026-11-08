# ImageChoice

Value object, a [`ResponseMode`](response-mode.md). The player selects from predefined image
answers. Holds correct answers, wrong answers and a [`ChoiceRequirement`](choice-requirement.md). An
answer is an image [`Media`](media.md) with an optional caption (1 to 200 characters, single line).

## Invariants

- 1 to 4 answers across both sets, at least one correct.
- No image appears in two answers. This also keeps an answer from being both correct and wrong.
- The media of an answer must be an image.
