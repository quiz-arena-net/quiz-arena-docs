# Features

Write side of the registry, exposed through `QuizAuthoringService`. Each feature lists its use
cases: actor, trigger, steps the application takes, the domain rules it relies on, and the ways it
can be rejected.

Common to every use case:

- The actor is an authenticated user. Presentation turns the verified token into a `Caller` (the
  user's `UserId` and roles), an application type. The domain only ever sees `UserId`.
- Authorization has two kinds. Who may run a use case at all is a role check at the top of the use
  case (`Caller::has_role`). Who may act on a given aggregate is a domain predicate
  (`is_editable_by`) that the application tests and turns into a rejection.
- A caller who may not act on an existing aggregate gets "forbidden", not "not found". Nothing in
  this context is secret enough to hide its existence.
- Each use case runs in one unit of work and reads the clock once. That time is passed into every
  domain operation of the use case, so one request stamps one time.
- Repository conflicts are retried up to three times, the same as greet. Rejections and internal
  failures are not retried.

| Feature | Use cases |
|---|---|
| [`author-quiz/`](author-quiz/usecase.md) | create, edit draft, discard draft, publish, change inclusion policy, delete |
| [`import-quiz/`](import-quiz/usecase.md) | import an external quiz |
| [`curate-quiz-list/`](curate-quiz-list/usecase.md) | create, change title / description / visibility / tags, add, remove, reorder, delete |
| [`browse-own-content/`](browse-own-content/usecase.md) | list my quizzes, list my quiz lists |

Read side (`QuizCatalogService`: view a list, resolve a list for a session, get a content version)
is not written yet.
