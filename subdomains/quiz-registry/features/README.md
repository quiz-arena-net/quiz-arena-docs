# Features

Write side of the registry, exposed through `QuizAuthoringService`. Each feature lists its use
cases: actor, trigger, steps the application takes, the domain rules it relies on, and the ways it
can be rejected. Statements marked **(assumed)** are working decisions, not confirmed requirements.

Common to every use case:

- The actor is an authenticated user. The application resolves the caller's `UserId` from the
  request, never from the payload.
- Each use case runs in one unit of work. Repository conflicts are retried up to three times
  **(assumed, same as greet)**. Rejections are not retried.
- Loading an aggregate the caller may not edit is reported as "not found" **(assumed)**, so the
  existence of other users' private content does not leak.

| Feature | Use cases |
|---|---|
| [`author-quiz/`](author-quiz/usecase.md) | create, edit draft, discard draft, publish, change inclusion policy, delete |
| [`import-quiz/`](import-quiz/usecase.md) | import an external quiz |
| [`curate-quiz-list/`](curate-quiz-list/usecase.md) | create, change title / description / visibility / tags, add, remove, reorder, delete |
| [`browse-own-content/`](browse-own-content/usecase.md) | list my quizzes, list my quiz lists |

Read side (`QuizCatalogService`: view a list, resolve a list for a session, get a content version)
is not written yet.
