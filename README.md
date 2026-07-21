# Quiz Arena Docs

Central documentation repository for the buzz quiz app: architecture, domain model, and decision
records. This repository contains cross-service documentation only (architecture, domain model, and
decisions that span service boundaries). Service-specific details live in each service's own
repository.

## Layout

```text
.
├── README.md
│
├── engineering/                   # cross-cutting engineering knowledge
│   ├── frontend/
│   ├── backend/
│   ├── integrations/
│   └── adr/
│
└── domains/                       # CORE: one directory per subdomain
    └── <subdomain>/
        ├── README.md              # context overview
        ├── models/                # one file per model element (entities, VOs, policies, ...)
        └── features/<name>/       # spec.md / usecase.md / sequence.md (as needed)
```

## Conventions

### Terminology

- In these docs, domain refers exclusively to the entire subject area of the project.
- Its divisions are always called subdomains (e.g. "the community subdomain", never "the community
  domain").
- The plural form appears only in the directory layout (`domains/`).

### Domain model

- Every model element (aggregate, entity, value object, policy, domain service) gets its own file in
  `domains/<subdomain>/models/`, named after the element in kebab-case (e.g. `answer-slot.md` for
  `AnswerSlot`). The file states the element's kind, role, and invariants.
- A policy is a named, swappable piece of domain rules with no identity of its own (a strategy or a
  domain service). The aggregate owns invariants. The policy only chooses among legal options.
- The subdomain directory's `README.md` is the context overview: it links the model files grouped by
  kind and lists the context's key events.

### Style

- No em-dashes and no semicolons in prose. Use a comma, colon, period, or parentheses instead.
  Semicolons remain allowed inside code blocks where the language requires them.

### Decision records

- ADRs are immutable once accepted.
- Supersede rather than edit (`Status: Superseded by ...`).

### Diagrams

- Diagrams are Mermaid blocks inside markdown so they render on GitHub.
