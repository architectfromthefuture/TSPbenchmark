# Task-Scope Preservation Benchmark

Task-Scope Preservation (TSP) is a candidate benchmark for the MIT Media Lab /
AHA Open Benchmark for the Human Impact of AI.

The benchmark evaluates whether an AI assistant preserves a user's
project-level objective across a constrained workflow instead of collapsing into
one visible subtask.

TSP v0 is a strict behavioral benchmark for detecting task-scope collapse. It is not a validated psychometric instrument and does not claim to establish population-level flourishing outcomes. Its purpose is to make one plausible mechanism of AI-mediated human impact observable: whether an assistant preserves the user's project-level objective, uncertainty state, and next actionable step under incomplete information.

In practice, scope preservation also means **joint-model-of-the-work** behavior:
keeping a shared picture of what is known, unknown, and worth clarifying next—especially under incomplete information—rather than substituting silent guesses where they would change the plan or mislead the user (see pass gate G10 in `rubric.md`).

## Submission Context

- Open Benchmark overview: <https://www.media.mit.edu/projects/the-open-benchmark-for-the-human-impact-of-ai/overview/>
- Project repository: <https://github.com/architectfromthefuture/TSPbenchmark>
- Related Open Benchmark ecosystem artifact (psychological-risk simulation, data + taxonomy): <https://github.com/mitmedialab/ai-psychosis>

## What TSP Measures

TSP scores whether a response:

- identifies the user's larger project objective;
- distinguishes the visible subtask from the full workflow;
- decomposes and sequences required work;
- names dependencies, validation checks, and recovery paths;
- avoids false completion signals; and
- reduces cognitive load with a concrete next action;
- passes **G10 (Evidence-bound inference)**: no unsupported bridging of missing facts as if they were known (see `rubric.md`).

For **multi-turn / dynamic** evaluation plans (Phase B), see `docs/dynamic_evaluation_notes.md` and `methodology.md`.

## Repository contents

- `prompts/` — v0 scenario records (JSONL)
- `scenarios/` — compact seed summaries and example generator output (JSONL)
- `judges/` — LLM-as-judge instructions
- `examples/` — positive and negative calibration examples
- `docs/` — submission draft and dynamic evaluation notes
- `behavior.md`, `methodology.md`, `rubric.md`, `failure_taxonomy.md`, `task_scope_preservation.schema.json`

## Related literature

Canonical references and DOIs: see [`CITATIONS.md`](CITATIONS.md).

## License

Copyright (c) 2026 Obversary Studios LLC. This repository is open source under the terms in [`LICENSE`](LICENSE) (MIT) for documentation and code-like text; benchmark data files under `prompts/` and `scenarios/` are additionally licensed under [`LICENSE-CC-BY-4.0.txt`](LICENSE-CC-BY-4.0.txt) (CC BY 4.0). See those files for attribution when redistributing data.

## Status

TSP v0 is a submission-ready behavioral benchmark artifact. It is not yet a
validated psychometric instrument.
