# FreeInputLlmJudge

Policy (strategy implementation): free text answer with an LLM verdict. Sits behind an
anti-corruption layer around the provider and needs an explicit timeout/failure
[`AttemptOutcome`](attempt-outcome.md). See ADR 0004.
