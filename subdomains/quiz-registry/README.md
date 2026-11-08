# Quiz Registry

Bounded context for the quiz content subdomain (supporting). Keeps the canonical copy of every quiz
and quiz list, turns drafts into immutable content versions on publish, and hands content out by
identifier to players and to other contexts. Discovery (search, rankings, likes) belongs to
Community & Discovery. Judging a player's answer belongs to Judging.

Implemented by the `registry` service. `QuizAuthoringService` is the write side for owners,
`QuizCatalogService` the read side for players and services.

## Aggregates

- [`Quiz`](models/quiz.md) (root): one question with its content versions and a draft
- [`QuizList`](models/quiz-list.md) (root): an ordered, versioned selection of quizzes

## Entities

- [`QuizContent`](models/quiz-content.md): one published version of a quiz
- [`QuizListEntries`](models/quiz-list-entries.md): one version of a list's ordered quizzes

## Value objects

Quiz content:

- [`DraftQuizContent`](models/draft-quiz-content.md)
- [`Prompt`](models/prompt.md) and [`PromptText`](models/prompt-text.md)
- [`CanonicalAnswer`](models/canonical-answer.md)
- [`ResponseMode`](models/response-mode.md): [`FreeInput`](models/free-input.md),
  [`TextChoice`](models/text-choice.md), [`ImageChoice`](models/image-choice.md),
  [`CharacterChoices`](models/character-choices.md), with
  [`ChoiceRequirement`](models/choice-requirement.md) and [`Character`](models/character.md)
- [`Media`](models/media.md)
- [`Tag`](models/tag.md) and [`TagSet`](models/tag-set.md)
- [`Source`](models/source.md) and [`SourceCredit`](models/source-credit.md)
- [`UsageTerms`](models/usage-terms.md), [`CreativeCommons`](models/creative-commons.md),
  [`CustomTerms`](models/custom-terms.md)
- [`WebUrl`](models/web-url.md)

Policies on the aggregates:

- [`InclusionPolicy`](models/inclusion-policy.md): whose lists may include a quiz
- [`Visibility`](models/visibility.md): who can reach a list

Quiz list text:

- [`QuizListTitle`](models/quiz-list-title.md)
- [`QuizListDescription`](models/quiz-list-description.md)

From the shared kernel:

- `UserId`: the owner of a quiz or list, or the author in a source. See the
  [shared kernel](../README.md#shared-kernel) in the subdomain overview.

## Repository ports

`QuizRepository` and `QuizListRepository` sit in the domain beside their aggregates: `find_by_id`,
`find_by_owner(owner, order, page)`, `add`, `update`, `remove(id)`. They return aggregates and have
no expected rejections. Identifiers are minted by the domain, and an aggregate that vanished between
a read and a write is a conflict. `Page<50>` comes from the shared kernel. The order type is per
aggregate (`QuizOrder`, `QuizListOrder`), today by creation or by last change.

## Modeling rules

- **Always valid.** Every type enforces its invariants in its constructor or through the types of
  its fields. A value that exists is a value that is allowed.
- **Drafts are typed.** Each publishable type has a `Draft*` counterpart that may leave fields empty
  but keeps every size limit. Converting a draft into its published form checks only what a draft
  may leave open: missing fields and conflicting entries.
- **Versions are the currency.** Publishing creates a new `QuizContent` with its own identifier.
  Changing a list's quizzes creates a new `QuizListEntries`. Other contexts bind to these
  identifiers, so later edits never change what they saw.
- **Entities compare by identifier, value objects by value.**
- **Text is normalized on entry.** Every text value is NFC. Single-line values are trimmed and
  reject newlines. All values reject control characters, blank text and text over their limit.

## Features

Use cases of the write side are in [`features/`](features/README.md).

## Key events (candidates, none emitted yet)

`QuizCreated`, `QuizPublished`, `QuizDeleted`, `QuizListCreated`, `QuizListEntriesChanged`,
`QuizListDeleted`

## Open points

- Attribution text for a user-authored quiz under a license that requires attribution: where the
  displayed name comes from, and what happens after the author leaves.
- Usage terms per media file, as opposed to one set of terms for the whole quiz.
- A quiz under a no-derivatives license can be edited and republished. The model cannot stop this,
  so the application has to.
- Whether tags fold case and width (`Tokyo`, `tokyo` and fullwidth `Ｔｏｋｙｏ` are three tags).
- Whether format characters other than the zero width joiner and non-joiner should be rejected in
  text values.
