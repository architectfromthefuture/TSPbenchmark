# Methodology Notes

These notes describe how Task-Scope Preservation can grow from a submission-ready
v0 benchmark into a research-grade behavioral evaluation.

## Evaluation pipeline

```text
behavior definition
-> scenario generation
-> execution against target model or agent
-> transcript capture
-> graded behavioral judgment
-> boundary failure labeling
-> suite-level reporting
```

## Scenario design

Each scenario should contain a mismatch between:

- the visible subtask the user asks about; and
- the project-level objective the assistant should preserve.

Good scenarios are realistic, constrained, and diagnosable. They should not
require hidden facts that no assistant could reasonably infer.

## Static and generated scenarios

TSP v0 uses static scenarios for repeatability and submission clarity. Future
versions should add generated scenario candidates, then manually select and edit
the best examples.

Generated scenarios should be filtered for:

- realistic user context;
- clear project objective;
- tempting visible subtask;
- identifiable failure boundaries;
- judgeable expected behavior;
- domain diversity; and
- absence of trick-question ambiguity.

## Execution

For each target model or assistant:

1. Present the `user_context` and `user_message`.
2. Capture the assistant response and relevant metadata.
3. Preserve the raw transcript.
4. Run a judge prompt or human rubric pass.
5. Store structured results.

Metadata should include model name, version if available, system prompt summary,
temperature or sampling settings when known, run timestamp, and evaluator version.

## Judging

TSP should support both binary and graded judging:

- **Binary v0**: PASS/FAIL for submission clarity.
- **Graded Phase B**: 1-5 scores on preservation dimensions.

Judge outputs should include rationales and failure labels. This prevents a
single aggregate score from hiding why a system failed.

## Reliability cautions

LLM-as-judge evaluation is useful for open-ended behavior, but it needs guardrails:

- tight construct definitions;
- concrete rubrics;
- calibration examples;
- structured output;
- disagreement review;
- spot checks by humans; and
- reporting of limitations.

Do not treat one judge response as ground truth. Treat it as one piece of
evaluation evidence.

## Multi-turn and dynamic evaluation

Static, single-turn prompts are valuable for repeatability and submission clarity.
They under-measure behaviors that only appear **across turns**: whether the system
**asks** when evidence is thin, **labels** assumptions, **accepts** user correction,
or **doubles down** on a wrong guess.

**Honest scope:** TSP v0 is evaluated as single-turn scenarios plus structured
judging (including pass gate G10). Full **dynamic** protocols—multi-turn
transcripts, injected reveals, or trajectory metrics—are **Phase B** and should be
documented separately (see `docs/dynamic_evaluation_notes.md`). Rationale for why
trajectory evaluation matters for assumption hygiene and agency (“static vs.
dynamic”) is summarized in [`../../../AHA_Submission.md`](../../../AHA_Submission.md)
when nested under `obversary-eval-harness`.

**Protocol sketch (Phase B, not required for v0):**

1. Fix a **turn budget** (for example 2-5 user turns).
2. Turn 1 uses the same scenario record as v0; capture the assistant reply.
3. Optionally **reveal** one missing fact the model assumed (or have the user
   correct it) and score whether the model **repairs** the plan versus defending
   unsupported inference.
4. Report **per-turn** G10 pass rate, **unsupported_inference** label rate, and
   optional **UAR** (see `rubric.md` / judge prompt) over the trajectory.

This design connects to human-impact evaluation: it rewards dialogue that
**widens the shared picture** of the task instead of **papering over gaps** with
fluent guesses.

## Suite-level reporting

Reports should include:

- total scenarios;
- pass rate;
- mean graded preservation score;
- false-done rate;
- validation inclusion rate;
- recovery inclusion rate;
- top failure labels;
- **G10 fail rate** (evidence-bound inference) on v0 runs;
- optional **UAR** or unsupported-assumption severity summaries when judges supply counts;
- representative failures; and
- limitations.

## Claims discipline

TSP can support claims such as:

- "System A preserved task scope on more v0 scenarios than System B."
- "Most failures for System A were dependency omissions."
- "The assistant often answered the visible subtask but missed validation."

TSP v0 should not support claims such as:

- "This assistant is generally safe."
- "This model understands user intent."
- "This benchmark proves human well-being impact."

Those claims require broader evidence, larger samples, human studies, and
validation work.

