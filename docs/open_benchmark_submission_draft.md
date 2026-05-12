# Open Benchmark Submission Draft: Task-Scope Preservation v0

## Benchmark name

Task-Scope Preservation (TSP): preserving project-level objectives under incomplete information

## Short description

Task-Scope Preservation evaluates whether an AI assistant preserves the user's project-level objective across a constrained workflow instead of collapsing into one narrow visible subtask.

## Submission target

This draft is structured for the MIT Media Lab / AHA Open Benchmark for the Human Impact of AI submission process.

- Open Benchmark overview: <https://www.media.mit.edu/projects/the-open-benchmark-for-the-human-impact-of-ai/overview/>
- Project repository: <https://github.com/architectfromthefuture/TSPbenchmark>
- Related process-oriented benchmark artifact: <https://github.com/mitmedialab/ai-psychosis>

## Motivation

Many AI assistants can produce plausible local answers while failing the user's actual intent. This is especially visible in project work: a user asks for a command, edit, metric, chart, or recommendation, but the underlying need is a workflow that includes sequencing, dependencies, validation, recovery, and honest uncertainty handling.

TSP measures that gap. It is designed to distinguish:

- a technically correct narrow answer; from
- a workflow-preserving response that helps the user continue the real project.

The benchmark's human-impact framing is practical: poor task-scope preservation can increase cognitive load, false confidence, over-reliance, and unfinished work. Good preservation supports autonomy, competence, self-efficacy, comprehension, and project completion.

TSP primarily targets the psychological and societal dimensions of human impact. Psychologically, it concerns cognitive load, confidence calibration, and the user's felt competence while navigating complex work. Societally, it concerns agency, learning, autonomy, and whether users remain active participants in AI-mediated workflows rather than becoming dependent on plausible but incomplete completions.

This directly fits the Open Benchmark project's emphasis on process-level evaluation: the relevant question is not only whether the model produces a correct answer, but whether the interaction pattern supports or undermines human capability development, agency, and comprehension over time.

## Construct

Task-Scope Preservation (TSP) measures whether an AI assistant preserves the user's project-level objective when the user's message emphasizes a narrow visible subtask.

In fuller terms, TSP measures joint model-of-the-work preservation: whether the assistant maintains a shared picture of what the user is trying to accomplish, what is known, what is unknown, what must happen next, and what should not be treated as complete yet. A response fails TSP when it gives a locally plausible answer while leaving the user with hidden sequencing burden, unverified assumptions, false "done" signals, or unsupported guesses that stand in for the user's actual context.

Operationally, a response preserves task scope when it:

1. recognizes the user's broader objective;
2. distinguishes the visible subtask from the full workflow;
3. decomposes the necessary components;
4. sequences the work;
5. surfaces dependencies and labeled assumptions;
6. includes validation or acceptance checks;
7. provides recovery or targeted clarification when missing facts would change the plan;
8. gives a concrete next action with low practical task latency; and
9. avoids implying that the project is complete when critical steps remain.

Pass gate G10, Evidence-bound Inference, adds an explicit epistemic requirement: the assistant must not fill decision-relevant gaps with unsupported bridging, such as invented repo state, platform, user intent, data shape, or environmental details. It should ground claims in what the user provided, label reasonable assumptions, or ask targeted clarification when the answer would materially change. Subordinate technical motivation from meta-awareness research appears under *Evidence basis and citations* and is not treated as evidence that training-time meta-awareness implies TSP outcomes.

## Behavioral vocabulary: observable human-supportive response patterns

TSP uses the following terms behaviorally, not affectively:

- Patience means deferring closure when missing facts could change the plan.
- Empathy operationalized means calibrating to uncertainty and stakes instead of replacing the user's context with fluent guessing.
- Inclusion means preserving user agency by integrating corrections and asking when decision-relevant.
- Grounding means separating evidence from assumption and giving actions the user can verify, revise, or undo.

These are not treated as subjective tone qualities. They are observable human-supportive response patterns that can be evaluated through the benchmark's pass gates and failure labels.

## Relation to existing constructs

TSP sits closest to the Open Benchmark framework's Reasoning, Comprehension, and Agency area. It operationalizes a concrete model behavior within that area: whether the model preserves the user's stated and implied intention across a workflow.

TSP relates to cognitive scaffolding, cognitive offloading, user intention modeling, context use, self-efficacy, competence, calibration, and automation over-reliance.

A TSP failure occurs when an assistant gives an answer that appears helpful but transfers hidden dependency, sequencing, or verification burden back to the user.

TSP is distinct from general reasoning benchmarks because it is not only about solving a problem. It is about preserving the shape of the user's work under incomplete information.

TSP is also distinct from broad safety benchmarks because it targets an everyday interaction failure: the model narrows the task too early, over-closes under ambiguity, or silently guesses the missing bridge between the user's request and the real workflow.

As a related process-oriented benchmark artifact, we note MIT Media Lab's ai-psychosis work as an example of simulated multi-turn risk evaluation:

- Repository: <https://github.com/mitmedialab/ai-psychosis>
- Explorer: <https://simulate.cyborglab.org/>
- Preprint: <https://arxiv.org/abs/2511.08880>

TSP is not the same construct and does not target severe psychological-risk pathways. TSP targets everyday project-scope collapse, epistemic discipline, and agency preservation in practical AI-assisted work.

## Evidence basis and citations

TSP v0 is a transparent behavioral benchmark artifact, not yet a validated psychometric instrument. Its initial evidence basis is conceptual and translational: it maps established human-impact concerns into an auditable model-behavior benchmark.

The construct is grounded in self-determination theory, especially autonomy and competence; cognitive load theory; and research on cognitive offloading to algorithms. TSP v0 does not claim to establish population-level flourishing outcomes by itself. It is intended to measure one plausible mechanism by which AI responses may support or undermine human flourishing: whether the model preserves the user's real task scope under uncertainty.

TSP is also informed by recent benchmark work emphasizing interactive and feedback-driven evaluation. RECODE-H argues that research-code development is poorly captured by one-shot evaluation and introduces multi-turn human-feedback interactions for evaluating LLM agents in realistic research implementation workflows. This supports TSP's methodological premise that assistant quality should be evaluated across workflow preservation, feedback integration, validation, and iteration rather than isolated answer correctness.

Recent work on meta-awareness in reasoning models also motivates TSP's evidence-bound inference gate. MASA studies the mismatch between predicted meta-information and true reasoning rollouts, arguing that models often lack reliable awareness of their own reasoning state. TSP does not evaluate internal model meta-awareness directly; instead, it evaluates an externally observable user-facing behavior: whether the assistant avoids unsupported bridging, marks uncertainty, and preserves the user's workflow under incomplete information.

Starting references for final submission review:

- MIT Media Lab / AHA workshop report *Final Next Steps for Benchmarks for Human Impact of AI* — process-level evaluation framing and the Reasoning, Comprehension, and Agency track (see Open Benchmark link above).
- Ryan, R. M., & Deci, E. L. (2000). Self-determination theory and the facilitation of intrinsic motivation, social development, and well-being. *American Psychologist*, 55(1), 68-78. https://doi.org/10.1037/0003-066X.55.1.68
- Sweller, J. (1988). Cognitive load during problem solving: Effects on learning. *Cognitive Science*, 12(2), 257-285. https://doi.org/10.1207/s15516709cog1202_4
- Wahn, B., Schmitz, L., Gerster, F. N., & Weiss, M. (2023). Offloading under cognitive load: Humans are willing to offload parts of an attentionally demanding task to an algorithm. *PLOS ONE*, 18(5), e0286102. https://doi.org/10.1371/journal.pone.0286102
- Zou, J., Poeppel, D., & Ding, N. (2026). Constituent-constrained word prediction during language comprehension. *Nature Neuroscience*. https://doi.org/10.1038/s41593-026-02272-6
- MIT Media Lab **ai-psychosis** — simulated multi-turn psychological-risk scenarios, model responses, and harmful-response taxonomy (Open Benchmark–adjacent human-impact artifact; interactive explorer at https://simulate.cyborglab.org/). https://github.com/mitmedialab/ai-psychosis (preprint: https://arxiv.org/abs/2511.08880)
- Miao, C., Zou, H. P., Li, Y., Chen, Y., Wang, Y., Wang, F., et al. (2025). RECODE-H: A Benchmark for Research Code Development with Interactive Human Feedback. arXiv:2510.06186. https://doi.org/10.48550/arXiv.2510.06186
- Kim, Y., Jang, D., & Yang, E. (2025). Meta-Awareness Enhances Reasoning Models: Self-Alignment Reinforcement Learning. arXiv:2510.03259. https://doi.org/10.48550/arXiv.2510.03259

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

TSP v0 is not limited to one demographic. The first seed set focuses on users engaged in multi-step AI-assisted project work, including:

- students;
- researchers;
- early-career professionals;
- independent builders;
- educators;
- developers; and
- people preparing public or consequential artifacts such as demos, submissions, reports, repositories, or decisions.

The benchmark especially concerns users who can ask a sharp sub-question but may not notice missing workflow steps, hidden dependencies, weak validation, or premature closure. These users may have enough domain knowledge to identify a goal, but still benefit from assistant behavior that preserves the full project scope.

Future scenario variants should explicitly vary domain expertise, time pressure, stakes, prior AI reliance, and simulated persona attributes where appropriate.

### Known user context

Each prompt record supplies a `user_context`, `project_objective`, and
`visible_subtask`. The model may know the user is working toward a larger project
but may receive a prompt that foregrounds only one visible subtask.

### Unknown user context

The model generally does not know the user's exact skill level, platform, stack, data state, deadline, tolerance for risk, previous failed attempts, unstated constraints, whether previous steps were validated, or whether the user will treat the assistant's answer as sufficient to stop working.

A scope-preserving response should handle that uncertainty by naming assumptions, avoiding false completion, and offering a safe next step or targeted clarification when a missing fact would change the correct workflow.

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
8. "What metric should I use to show this assistant is actually helping users?"

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
- practical task latency;
- completion honesty; and
- evidence-bound inference, G10.

Any missing gate produces a FAIL. This intentionally sets a high bar: the
benchmark is designed to detect cases where a response sounds helpful while
leaving the project incomplete.

For v0, the gates are intentionally strict because TSP is designed to detect scope collapse. Future calibration may relax or weight gates depending on scenario type, judge reliability, and empirical pilot results.

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

