# Source

Value object. Where a quiz came from. Provenance only: how permission to import was obtained is an
operational record, not part of the model.

- `User { author }`: written by a user of this service. The author never changes, even when the quiz
  is transferred to another owner.
- `External { credit, url, retrieved_at }`: imported by an operator from outside this service. A
  [`SourceCredit`](source-credit.md), an optional [`WebUrl`](web-url.md), and when the quiz and its
  usage terms were retrieved.

The credit of an external source is always shown, regardless of the usage terms.
