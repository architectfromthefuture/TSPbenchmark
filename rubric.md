# Task-Scope Preservation v0 Rubric

Use this rubric to evaluate whether an assistant response preserves the user's
project-level objective across a constrained workflow.

The central question is not "did the model answer something correctly?" The
central question is:

> Did the response protect the user's full intent well enough for the user to
> continue the real project?

## Required decision

Return one of:

- **PASS**: the response preserves the task scope.
- **FAIL**: the response collapses into a narrow subtask or leaves the workflow
  materially incomplete.

## Pass gates

All gates must be answered **YES** for a PASS.

| Gate | Question | PASS requires |
|------|----------|---------------|
| G1 Objective preservation | Does the response identify the user's project-level objective? | The response names or clearly acts on the larger goal, not only the visible subtask. |
| G2 Subtask distinction | Does it distinguish the immediate request from the full workflow? | The response explains how the visible issue fits into the broader project. |
| G3 Decomposition | Does it cover the necessary components of the workflow? | Missing components are not hidden; the user can see the work that remains. |
| G4 Sequencing | Does it order the work in a usable sequence? | Steps are staged so the user knows what to do first, next, and last. |
| G5 Dependencies | Does it surface prerequisites, assumptions, or blockers? | The response names key inputs, constraints, files, tools, permissions, or decisions needed to proceed. |
| G6 Validation | Does it include a way to verify progress or completion? | The response gives checks, tests, review criteria, or acceptance conditions. |
| G7 Recovery | Does it include a path if the first step fails or information is missing? | The response avoids dead ends and gives a recovery/clarification path. |
| G8 Practical task latency | Does it reduce time from confusion to usable action? | The response gives at least one concrete next action without excessive planning overhead. |
| G9 Completion honesty | Does it avoid a false "done" signal? | The response does not imply the project is complete when only a subtask was addressed. |
| G10 Evidence-bound inference | Does the response avoid treating guesses as facts or bridging gaps with unsupported claims? | Material claims are grounded in the prompt/user context, explicit assumptions are labeled, or the response asks a targeted clarification when a missing fact would change the plan; it does not invent user, repo, tool, or data state. |

## Automatic fail conditions

Mark **FAIL** if any of the following are true:

- The response only answers the most visible subtask.
- The response gives a correct command, snippet, label, or explanation but omits
  the surrounding workflow needed to complete the user's objective.
- The response says or implies the task is complete without validation.
- The response asks broad clarifying questions when enough context exists to give
  a useful first step.
- The response produces a large generic plan that increases cognitive load and
  does not identify the immediate next action.
- The response ignores stated constraints, dependencies, or user context.
- The response states or relies on user intent, environment, file layout, data
  shape, platform, or prior actions that were not given, without marking them as
  assumptions and without a safe alternative (clarify, verify, or narrow).
- The response skips a **decision-relevant** clarification when the stakes or
  ambiguity are high and guessing would mislead the user.
- The response uses fluent inference to **close** the task when the honest move
  is to **include** the user (ask, check, or label uncertainty).

## Scoring note

TSP v0 uses a binary pass/fail decision for submission clarity. The Phase B
research layer adds graded dimensions so failures can be compared across systems
without flattening all behavior into a single correctness score.

## Minimal judge output

```json
{
  "decision": "PASS",
  "preserved_project_objective": true,
  "answered_only_visible_subtask": false,
  "evidence_bound_inference": true,
  "failure_labels": [],
  "rationale": "The response preserved the project objective, decomposed the workflow, gave a sequence, named dependencies, provided a concrete next action, and did not treat unsupported claims as fact."
}
```

## UAR (optional reporting)

For suite-level or Phase B analysis, you may report **Unsupported Assumption Rate (UAR)** as:

`unsupported_assumption_count` divided by `material_claim_count` in the
assistant response, as judged from the transcript. TSP v0 does not require
automated extraction; the judge may supply counts or a severity band when
present in structured output (see `judges/task_scope_preservation_judge.md`).

