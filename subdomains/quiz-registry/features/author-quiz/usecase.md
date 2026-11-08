# Author a quiz

Actor: a user working on their own quiz. Aggregate: [`Quiz`](../../models/quiz.md).

## Create a quiz

- Trigger: the user starts a new quiz.
- Input: a draft (any field may be empty), the language, usage terms, inclusion policy.
- Steps: build `DraftQuizContent` with `Source::User { author: caller }`, call
  `Quiz::new(caller, draft, inclusion_policy, now)`, `QuizRepository::add`.
- No server-side defaults. Usage terms and inclusion policy are required input. What the client
  preselects is the client's decision.
- Rejected when: a text field fails to parse, a draft limit is exceeded (tags, answers, positions).
- Outcome: an unpublished quiz with its identifier. Nothing is visible to anyone but the owner.

## Edit the draft

- Trigger: the user saves changes to a quiz.
- Steps: `find_by_id`, `is_editable_by(caller)`, `Quiz::edit_draft(draft, now)`, `update`.
- The whole draft is replaced. There is no field-level patching. Two devices editing the same draft
  end with the later save.
- Rejected when: not found, forbidden, a text field fails to parse, a draft limit is exceeded.

## Discard the draft

- Trigger: the user drops unpublished changes of a published quiz.
- Steps: `find_by_id`, `is_editable_by`, `Quiz::discard_draft(now)`, `update`.
- Rejected when: the quiz has no draft, or is unpublished (use delete instead).

## Publish

- Trigger: the user publishes the draft.
- Steps: `find_by_id`, `is_editable_by`, `Quiz::publish(now)`, `update`. The repository stores the
  new `QuizContent` as a new version and keeps the old ones.
- Rejected when: there is no draft, or the draft is not ready. Every missing or conflicting item is
  reported at once (`PublishError::DraftNotReady`).
- Outcome: a new content version. Lists that include the quiz now serve the new version when a
  session starts. Running sessions keep the version they started with.
- Open: a quiz imported under a no-derivatives license is republished as an adapted work. The
  application has to block this. Rule not yet defined.

## Change the inclusion policy

- Steps: `find_by_id`, `is_editable_by`, `Quiz::change_inclusion_policy(policy, now)`, `update`.
- Outcome: takes effect at the next list addition and the next session start. Existing list entries
  that are no longer permitted stay in the list and are skipped.

## Delete

- Trigger: the user deletes a quiz.
- Steps: `find_by_id`, `is_editable_by`, `QuizRepository::remove(id)`.
- Hard delete, including every content version. Soft delete and retraction are out of scope. The
  repository may keep a copy in an archive table (infrastructure only, read nowhere).
- Lists keep the identifier and skip it when a session resolves them. Statistics keep their version
  identifiers and show the quiz as deleted when the content cannot be found.
- Allowed while the quiz is in other users' lists and while sessions are running. A session resolved
  its content versions at start and does not read the registry afterwards.

## Repository needs

`QuizRepository::find_by_id`, `add`, `update`, `remove`.
