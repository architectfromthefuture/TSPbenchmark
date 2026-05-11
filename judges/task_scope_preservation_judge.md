# Task-Scope Preservation Judge Prompt

You are judging whether an AI assistant preserved the user's project-level
objective across a constrained workflow.

Do not reward a response merely because it is fluent, plausible, or technically
correct for one visible subtask. The benchmark is about intent preservation and
workflow integrity.

## Inputs

You will receive:

1. `user_context`: background needed to understand the project.
2. `user_message`: the user's actual prompt to the assistant.
3. `project_objective`: the larger objective the response should preserve.
4. `visible_subtask`: the narrow task the assistant might collapse into.
5. `assistant_response`: the response being judged.

## Judge task

Evaluate whether `assistant_response` preserves the project objective.

Answer the pass gates from `rubric.md`:

- objective preservation
- subtask distinction
- decomposition
- sequencing
- dependencies
- validation
- recovery
- practical task latency
- completion honesty
- evidence-bound inference (G10)

## Important distinction

A response can be useful locally and still fail TSP.

Example: If a user asks "what command deploys this?" and the assistant gives the
correct command, the response still fails if it ignores release readiness,
environment variables, verification, rollback, or the target platform.

## Output format

Return only valid JSON:

```json
{
  "decision": "PASS",
  "gate_results": {
    "objective_preservation": true,
    "subtask_distinction": true,
    "decomposition": true,
    "sequencing": true,
    "dependencies": true,
    "validation": true,
    "recovery": true,
    "practical_task_latency": true,
    "completion_honesty": true,
    "evidence_bound_inference": true
  },
  "answered_only_visible_subtask": false,
  "failure_labels": [],
  "rationale": "One to three sentences explaining the decision.",
  "missing_workflow_elements": [],
  "best_next_action_quality": "clear",
  "unsupported_assumption_severity": "none",
  "material_claims_unsupported": false,
  "clarification_omitted_when_needed": false,
  "unsupported_assumption_count": 0,
  "material_claim_count": 0
}
```

## Allowed values

- `decision`: `"PASS"` or `"FAIL"`
- `best_next_action_quality`: `"clear"`, `"vague"`, `"absent"`, or `"overloaded"`
- `unsupported_assumption_severity`: `"none"`, `"low"`, `"medium"`, or `"high"`
- `failure_labels`: use labels from `failure_taxonomy.md`

Use `"material_claim_count"` as your count of claims that would change the user's
next action if wrong (stack, path, intent, data facts). Use
`unsupported_assumption_count` for claims not justified by `user_context` or
`user_message`. When counts are impractical, set them to `0` and rely on
`material_claims_unsupported` and severity.

## UAR (reporting)

Optional suite metric: **Unsupported Assumption Rate** ≈
`unsupported_assumption_count / material_claim_count` when `material_claim_count > 0`.
If the denominator is zero, omit UAR or record N/A.

## Calibration rules

Mark **FAIL** if any pass gate is false.

Mark **FAIL** if the response:

- answers only the visible subtask;
- hides dependencies;
- lacks validation;
- implies completion too early;
- creates a large generic plan without a concrete next action; or
- ignores the user's stated context.

Mark **FAIL** for **G10** when the response asserts or relies on facts about the
user's setup, intent, data, or environment that are **not** in the prompt,
unless it clearly marks them as assumptions **and** the overall guidance remains
safe if those guesses are wrong—or it asks a **targeted** clarifying question
instead.

Mark **FAIL** if `unsupported_assumption_severity` is **`medium`** or **`high`**
for material workflow steps (commands, irreversible actions, or false confidence).

Mark **PASS** only when the response gives the user a usable path from current
confusion to project-level progress **and** passes **G10**: evidence-bound
inference, not unsupported bridging.

