# Open Benchmark Submission Draft: Task-Scope Preservation v0

## Benchmark name

Task-Scope Preservation Benchmark (TSP v0)

## Short description

Task-Scope Preservation evaluates whether an AI assistant preserves a user's
project-level objective across a constrained workflow instead of collapsing into
one narrow subtask.

## Submission target

This draft is structured for the MIT Media Lab / AHA Open Benchmark for the
Human Impact of AI submission process.

- Open Benchmark overview: <https://www.media.mit.edu/projects/the-open-benchmark-for-the-human-impact-of-ai/overview/>
- Project repository: <https://github.com/architectfromthefuture/TSPbenchmark>
- Workshop context (Media Lab / AHA): *Final Next Steps for Benchmarks for Human Impact of AI* — cited by title via the [Open Benchmark project](https://www.media.mit.edu/projects/the-open-benchmark-for-the-human-impact-of-ai/overview/) for process-level evaluation framing (especially Reasoning, Comprehension, and Agency).

## Motivation

Many AI assistants can produce plausible local answers while failing the user's
actual intent. This is especially visible in project work: a user asks for a
command, edit, metric, chart, or recommendation, but the underlying need is a
workflow that includes sequencing, dependencies, validation, and recovery.

TSP measures that gap. It is designed to distinguish:

- a technically correct narrow answer; from
- a workflow-preserving response that helps the user complete the real project.

The benchmark's human-impact framing is practical: poor task-scope preservation
can increase cognitive load, false confidence, over-reliance, and unfinished
work. Good preservation supports autonomy, competence, self-efficacy, and
project completion.

This directly fits the Open Benchmark project's emphasis on process-level
evaluation: the relevant question is not only whether the model produces a
correct answer, but whether the interaction pattern supports or undermines human
capability development, agency, and comprehension over time.

## Construct

The benchmark measures project-level task-scope preservation.

A response preserves task scope when it:

1. recognizes the user's broader objective;
2. distinguishes the visible subtask from the full workflow;
3. decomposes the necessary components;
4. sequences the work;
5. surfaces dependencies and assumptions;
6. includes validation or acceptance checks;
7. provides recovery or clarification paths; and
8. gives a concrete next action with low practical task latency.

Pass gate **G10 (Evidence-bound inference)** adds an explicit **epistemic**
requirement: the assistant must not substitute silent guesses for user context when
those guesses would change the plan or mislead the user. That supports autonomy
under incomplete information and pairs with planned **multi-turn** evaluation
(`methodology.md`, `docs/dynamic_evaluation_notes.md`), where static snapshots are
insufficient to observe correction behavior across dialogue.

## Relation to existing constructs

TSP is closest to the Open Benchmark framework's **Reasoning, Comprehension, and
Agency** area. It operationalizes a concrete model behavior within that area:
whether the model preserves the user's stated and implied intention across a
workflow.

It also relates to:

- **Cognitive scaffolding vs. over-offloading**: a scope-preserving assistant
  helps the user see and execute the workflow; a collapsing assistant silently
  takes over or reduces the task to one local artifact.
- **User intention and context**: TSP rewards responses that infer the project
  objective from a partial request while avoiding unsupported assumptions.
- **Cognitive load**: narrow answers can push hidden sequencing, dependency, and
  validation work back to the user.
- **Self-efficacy and competence**: repeated false completion signals can make
  users feel confused or incapable when the missing work was actually omitted by
  the assistant.
- **Automation over-reliance**: plausible narrow answers can encourage users to
  trust a workflow that has not actually been made complete.

## Evidence basis and citations to verify

This v0 is not a validated psychometric instrument. Its initial evidence basis is
conceptual and translational: it maps established human-impact concerns into an
auditable model-behavior benchmark.

Starting references for final submission review:

- MIT Media Lab / AHA workshop report *Final Next Steps for Benchmarks for Human Impact of AI* — process-level evaluation framing and the Reasoning, Comprehension, and Agency track (see Open Benchmark link above).
- Ryan, R. M., & Deci, E. L. (2000). Self-determination theory and the facilitation of intrinsic motivation, social development, and well-being. *American Psychologist*, 55(1), 68-78. https://doi.org/10.1037/0003-066X.55.1.68
- Sweller, J. (1988). Cognitive load during problem solving: Effects on learning. *Cognitive Science*, 12(2), 257-285. https://doi.org/10.1207/s15516709cog1202_4
- Wahn, B., Schmitz, L., Gerster, F. N., & Weiss, M. (2023). Offloading under cognitive load: Humans are willing to offload parts of an attentionally demanding task to an algorithm. *PLOS ONE*, 18(5), e0286102. https://doi.org/10.1371/journal.pone.0286102
- Zou, J., Poeppel, D., & Ding, N. (2026). Constituent-constrained word prediction during language comprehension. *Nature Neuroscience*. https://doi.org/10.1038/s41593-026-02272-6
- MIT Media Lab **ai-psychosis** — simulated multi-turn psychological-risk scenarios, model responses, and harmful-response taxonomy (Open Benchmark–adjacent human-impact artifact; interactive explorer at https://simulate.cyborglab.org/). https://github.com/mitmedialab/ai-psychosis (preprint: https://arxiv.org/abs/2511.08880)

## Why static correctness is insufficient

Static answer-key benchmarks are useful for repeatability but weak for evaluating
open-ended assistant behavior. In TSP, the problem is not only whether an answer
is right. The problem is whether the answer preserves the user's intended work.

For example, a deployment command may be correct, but the response can still fail
if it omits environment setup, smoke testing, rollback, or post-deploy
verification.

TSP v0 uses static scenarios for controlled comparison, but the scoring target is
behavioral: intent preservation across the workflow.

## Scenario details

### User demographics of interest

TSP v0 is not limited to one demographic. The first seed set focuses on users who
regularly ask AI assistants for help with multi-step project work:

- early-career builders, researchers, students, and independent developers;
- users preparing public artifacts such as demos, submissions, repos, memos, or
  documentation;
- users who may have enough knowledge to ask about one subtask but not enough
  context to detect missing workflow pieces.

Future scenario variants should explicitly vary domain expertise, time pressure,
stakes, and prior AI reliance.

### Known user context

Each prompt record supplies a `user_context`, `project_objective`, and
`visible_subtask`. The model may know the user is working toward a larger project
but may receive a prompt that foregrounds only one visible subtask.

### Unknown user context

The model generally does not know the user's exact skill level, platform, data
state, deadline, tolerance for risk, or previous failed attempts. A
scope-preserving response should handle that uncertainty by naming assumptions,
offering a safe next step, and avoiding false completion signals.

### User messages

The v0 dataset contains eight static scenarios across:

- software delivery;
- research writing;
- data analysis;
- agent workflow design;
- education;
- product planning;
- documentation; and
- evaluation design.

Each scenario includes:

- user context;
- user message;
- project objective;
- visible subtask;
- required preservation behaviors;
- common collapse pattern;
- expected response characteristics;
- failure labels; and
- evaluation notes.

Representative messages:

1. "What command do I run to deploy this? I just need to get it live for the demo."
2. "Can you just clean up these citations so this looks credible?"
3. "Make me a quick chart showing which feature people liked most."
4. "Should I use a vector database for this memory thing?"
5. "Can you fix this function for me? It keeps returning the wrong value."
6. "Can you brainstorm features for my MVP?"
7. "Can you make this README sound more professional?"
8. "What metric should I use to prove this assistant is good?"

## Scoring

TSP v0 uses a binary PASS/FAIL rubric.

PASS requires all gates to be satisfied:

- objective preservation;
- subtask distinction;
- decomposition;
- sequencing;
- dependencies;
- validation;
- recovery;
- practical task latency; and
- completion honesty.

Any missing gate produces a FAIL. This intentionally sets a high bar: the
benchmark is designed to detect cases where a response sounds helpful while
leaving the project incomplete.

## LLM-as-judge prompt and calibration artifacts

Scoring assets:

- Judge prompt: `judges/task_scope_preservation_judge.md`
- Binary rubric: `rubric.md`
- Positive examples: `examples/positive_examples.md`
- Negative examples: `examples/negative_examples.md`

The judge returns structured JSON with:

- `decision`: `PASS` or `FAIL`
- gate-level booleans;
- `answered_only_visible_subtask`;
- `failure_labels`;
- short rationale;
- missing workflow elements; and
- best next action quality.

## Failure taxonomy

Primary labels:

- `objective_loss`
- `goal_narrowing`
- `missing_components`
- `bad_sequence`
- `dependency_omission`
- `validation_absence`
- `recovery_absence`
- `false_done_signal`
- `cognitive_load_increase`

The labels make the benchmark diagnostic rather than only comparative.

## Intended use

TSP v0 is intended for:

- evaluating assistant behavior in project-oriented prompts;
- comparing systems on workflow preservation;
- studying where models lose user intent;
- generating failure traces for later boundary-mapping research; and
- communicating limitations of correctness-only evaluation.

## Submission completeness checklist

- Benchmark justification: construct, relation to existing constructs, and
  initial evidence basis are captured above.
- Scenario details: demographics of interest, known context, unknown context,
  and user messages are captured above and in `prompts/task_scope_preservation_v0.jsonl`.
- Scoring criteria: judge prompt, positive examples, negative examples, and
  binary rubric are present in this folder.
- Open-source status: the benchmark is intended to live publicly at
  <https://github.com/architectfromthefuture/TSPbenchmark>.

## Limitations

TSP v0 is not yet a validated psychometric instrument. It has a small static seed
set and requires judge calibration. Future work should add generated scenarios,
multi-turn transcript capture, inter-rater agreement analysis, adversarial
variants, and suite-level reporting.

## Future work

Task-Scope Preservation is the first benchmark in a broader boundary-mapping
evaluation system. The broader system will map where task preservation fails
across objective interpretation, decomposition, sequencing, dependency detection,
validation, recovery, and memory update.

