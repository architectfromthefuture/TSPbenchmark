# Task-Scope Preservation Benchmark

- TSP is a candidate benchmark for the MIT Media Lab / AHA Open Benchmark for the Human Impact of AI.
- TSP evaluates whether an AI assistant preserves a user's project-level objective across a constrained workflow instead of collapsing into one visible subtask.

TSP v0 is a strict behavioral benchmark for detecting task-scope collapse. It is not a validated psychometric instrument and does not claim to establish population-level flourishing outcomes. Its purpose is to make one plausible mechanism of AI-mediated human impact observable: whether an assistant preserves the user's project-level objective, uncertainty state, and next actionable step under incomplete information.

In practice, scope preservation also means **joint-model-of-the-work** behavior: keeping a shared picture of what is known, unknown, and worth clarifying next—especially under incomplete information—rather than substituting silent guesses where they would change the plan or mislead the user (see pass gate G10 in `rubric.md`).

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
- avoids false completion signals;
- reduces cognitive load with a concrete next action; and
- passes **G10, Evidence-bound Inference**: no unsupported bridging of missing facts as if they were known (see `rubric.md`).

In practical terms, TSP asks whether the assistant preserves the user's real work without inventing missing context, prematurely narrowing the task, or signaling completion before the workflow is actually ready.

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

## Citation

If you use Task-Scope Preservation (TSP v0) in research, evaluation, reporting, or benchmark comparison work, please cite it as:

```bibtex
@misc{moran2026tspbenchmark,
  author = {Brian Moran},
  title = {Task-Scope Preservation Benchmark (TSP v0)},
  year = {2026},
  publisher = {Obversary Studios LLC},
  url = {https://github.com/architectfromthefuture/TSPbenchmark},
  note = {Open-source benchmark artifact for evaluating task-scope preservation and evidence-bound inference in AI assistant responses}
}
```

Citation metadata is also available in [`CITATION.cff`](CITATION.cff).

## License

This repository uses split licensing:

- Code-like materials, schemas, documentation, methodology notes, rubric text, and judge templates are licensed under the MIT License.
- Benchmark data and reusable evaluation content under `prompts/`, `scenarios/`, and `examples/` are licensed under Creative Commons Attribution 4.0 International (CC BY 4.0).

See [`LICENSE`](LICENSE), [`LICENSE-CC-BY-4.0.txt`](LICENSE-CC-BY-4.0.txt), and [`CITATION.cff`](CITATION.cff).

## Status

TSP v0 is a submission-ready behavioral benchmark artifact. It is not yet a validated psychometric instrument.
