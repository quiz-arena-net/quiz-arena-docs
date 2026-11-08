# QuizContent

Entity inside [`Quiz`](quiz.md). One published version of a quiz's content, identified by its own
`QuizContentId`, assigned on every publication. Two versions with identical content are still
distinct versions.

Holds a [`Prompt`](prompt.md), a [`CanonicalAnswer`](canonical-answer.md), exactly one
[`ResponseMode`](response-mode.md), a language (ISO 639), a [`TagSet`](tag-set.md), a
[`Source`](source.md) and [`UsageTerms`](usage-terms.md).

## Invariants

All carried by the field types. Construction cannot fail.

## Conversion from a draft

`QuizContent::try_from(DraftQuizContent)` reports every violation at once: missing prompt text,
missing canonical answer, missing response mode, response mode not ready.

## Persistence note

The aggregate holds only the latest version. Every version has to be kept by the repository, because
sessions and statistics refer to version identifiers.
