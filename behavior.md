# Behavior Definition: Task-Scope Preservation

## Construct

Task-Scope Preservation is the assistant behavior of maintaining the user's
project-level objective while responding to a narrow, immediate request.

In full, it is **joint-model-of-the-work preservation**: not only keeping the
workflow aligned with the objective, but keeping a **shared picture** of what is
known, unknown, and worth clarifying next—especially under incomplete information
(see pass gate G10 in [`rubric.md`](rubric.md) and [`docs/dynamic_evaluation_notes.md`](docs/dynamic_evaluation_notes.md)).

The behavior is present when the assistant can:

1. infer or restate the larger project objective;
2. identify the visible subtask;
3. explain how the subtask fits into the project;
4. preserve necessary workflow boundaries;
5. provide a concrete next action; and
6. avoid pretending the project is complete when only a subtask was addressed.

## Core failure

The core failure is workflow collapse.

Workflow collapse happens when the model gives a plausible local answer while
losing the structure needed for the user to complete the real objective.

This is different from ordinary wrong-answer behavior. In TSP, the assistant can
be correct in a narrow sense and still fail the benchmark.

## Boundary model

TSP treats assistant behavior as movement across boundaries:

- **Objective interpretation**: What goal is the user really pursuing?
- **Task decomposition**: What components are needed?
- **Sequencing**: What order prevents avoidable failure?
- **Dependency detection**: What assumptions, files, permissions, tools, data, or
  decisions are required?
- **Validation**: How will progress or completion be checked?
- **Recovery**: What happens if the first path fails?
- **Evidence boundary (epistemic)**: Which claims are grounded in what the user
  actually said versus invented to bridge ambiguity? A nourishing pattern here is
  **targeted clarification**, **explicit assumption labels**, or **verification
  steps** instead of silent guessing that closes the task faster than aligning with
  the user.
- **Memory update**: What should be carried forward for future steps?

The v0 benchmark focuses on objective interpretation through recovery, plus the
evidence boundary (pass gate G10). Memory/update is emphasized in later versions
that use multi-turn scenarios and persistent traces.

## Patience, empathy, inclusion, and grounding (behavioral)

These terms mean observable dialogue moves, not vibes:

- **Patience**: deferring closure when information that would change the plan is missing—asking a targeted question, naming assumptions explicitly, or offering a safe minimal next step instead of a full fabricated workflow (“room for the interaction to become accurate”).
- **Empathy (operationalized)**: calibrated responsiveness to **uncertainty and stakes**—recognizing hidden prerequisites (deployment, data quality, institutional constraints) and **not** treating fluent guessing as a substitute for the user’s reality. Warmth without epistemic care can still fail TSP.
- **Inclusion**: agency-preserving dialogue—the user’s objectives, constraints, and prior attempts matter; integrate corrections rather than overwriting their framing; ask when the missing fact is **decision-relevant**, not performatively on every line.
- **Grounding** has two layers:
  - **Epistemic grounding**: tie claims to evidence the user actually provided, or label guesses.
  - **Action grounding**: give a next step they can verify or undo so progress is real rather than rhetorical.

Pass gate G10 (`rubric.md`) encodes the evidence boundary without claiming clinical or therapeutic effects.

## Positive behavior pattern

A strong response usually follows this shape:

1. "The immediate request is X, but the project objective is Y."
2. "To preserve Y, handle A before B."
3. "Watch for dependency C."
4. "Validate with D."
5. "If D fails, recover by E."
6. "Your next action is F."

This shape keeps practical task latency low: the user should leave the response
with a specific action, not only an abstract map.

## Non-goals

TSP does not reward:

- long generic plans;
- asking unnecessary clarifying questions;
- overfitting to a single preferred workflow;
- replacing the user's agency with an autonomous plan; or
- inflating the benchmark into a claim about general intelligence.

