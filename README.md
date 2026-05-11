# Task-Scope Preservation Benchmark

Task-Scope Preservation (TSP) is a candidate benchmark for the MIT Media Lab /
AHA Open Benchmark for the Human Impact of AI.

The benchmark evaluates whether an AI assistant preserves a user's
project-level objective across a constrained workflow instead of collapsing into
one visible subtask.

## Submission Context

- Open Benchmark overview: <https://www.media.mit.edu/projects/the-open-benchmark-for-the-human-impact-of-ai/overview/>
- Project repository: <https://github.com/architectfromthefuture/TSPbenchmark>
- Source workspace: `benchmarks/task_scope_preservation/` inside `obversary-eval-harness`
- Related Open Benchmark ecosystem artifact (psychological-risk simulation, data + taxonomy): <https://github.com/mitmedialab/ai-psychosis>
- Harness working notes (patience / empathy / inclusion / grounding; static vs. dynamic): when checked out inside **Obversary Evaluation Harness**, see [`../../../AHA_Submission.md`](../../../AHA_Submission.md); standalone mirrors use the harness repo for that file.

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

## Status

TSP v0 is a submission-ready behavioral benchmark artifact. It is not yet a
validated psychometric instrument.

The current source workspace contains:

- prompt records;
- JSON schema;
- binary rubric;
- LLM-as-judge prompt;
- positive and negative examples;
- failure taxonomy;
- Open Benchmark submission draft; and
- methodology notes for later transcript-based evaluation.

When this standalone repository is populated, copy only the TSP-specific files
from the source workspace and preserve the honest scope above.
