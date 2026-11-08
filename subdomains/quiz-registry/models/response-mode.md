# ResponseMode

Value object. The way players respond to a quiz. Exactly one of [`FreeInput`](free-input.md),
[`TextChoice`](text-choice.md), [`ImageChoice`](image-choice.md) or
[`CharacterChoices`](character-choices.md).

Each mode has a `Draft*` counterpart. Drafts may leave sets empty and may hold conflicting entries
(an answer that is both correct and wrong, an image used twice, a correct character among the wrong
ones) but keep every size limit. Converting a draft reports the first missing or conflicting entry.

How a response is judged is configured by the session, not here. The judging context receives the
mode as its answer key.
