# Import a quiz

Actor: an operator. Aggregate: [`Quiz`](../../models/quiz.md).

## Import an external quiz

- Trigger: an operator brings a quiz from outside the service, for example from a site whose terms
  allow reuse.
- Who is an operator: the `Operator` role on the `Caller`, granted in Identity. The application
  checks it. The domain does not know roles.
- Input: the draft, the language, `Source::External { credit, url, retrieved_at }`, usage terms,
  inclusion policy.
- Steps: same as create, with the external source. The owner is the shared operations account, not
  the operator who ran the import, so ownership survives staff changes. `retrieved_at` is the time
  the operator checked the source, supplied by the application.
- No server-side defaults. The inclusion policy is required input.
- Rejected when: the caller is not an operator, or any create rejection.
- Outcome: an unpublished quiz owned by the operations account. Publishing follows the author-quiz
  flow.

## Notes

- How permission to import was obtained is recorded outside the model (operations log).
- Usage terms are what users see. `AllRightsReserved` is the right value when the source states no
  terms, even if the operator obtained permission.
- Imports in bulk are a loop over this use case, one unit of work each. No batch operation in the
  domain. A failure in the middle leaves the earlier imports in place.

## Repository needs

`QuizRepository::add`.
