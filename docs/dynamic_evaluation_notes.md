# Dynamic evaluation notes (Phase B stub)

This file reserves space for **multi-turn / trajectory** evaluation of Task-Scope
Preservation. It does **not** claim that dynamic runs are implemented in the v0
artifact.

## Purpose

Single-turn scenarios score what the model does in one shot. Many human-impact
constructs—**trust calibration**, **assumption hygiene**, **respect for unknowns**—live
in **trajectories**, not snapshots: single-turn setups can reward plausible closure
and under-reward appropriate clarification because turn two never happens.

Many behaviors—including **evidence-bound inference** (pass gate G10)—appear more
clearly when the user can **correct**, **clarify**, or **reveal** missing facts
across turns.

### Static vs. dynamic signals (sketch)

| Static (single-shot) signal | Dynamic (multi-turn) signal |
|------------------------------|------------------------------|
| One good-looking answer | Repeated unsupported bridges across turns |
| “Helpful” tone | Whether it asks when stakes are high vs. infers when clarification is cheap |
| Pass/fail on rubric once | Whether it honors corrections or overwrites user framing |

**Escalation:** assumption severity can rise when the user pushes back—so **UAR-style**
metrics become **trajectory** statistics: not only “did this sentence invent X?” but
“does this agent habitually infer before aligning?”

## Links

- Construct and boundaries: [`behavior.md`](../behavior.md)
- Multi-turn methodology sketch: [`methodology.md`](../methodology.md)
- Rubric gates G1–G10: [`rubric.md`](../rubric.md)

## Placeholders (to define in Phase B)

- Transcript JSON shape (roles, turn index, tool calls if any).
- When to inject a **user correction** versus an **environment reveal**.
- Trajectory-level metrics: G10 pass rate per turn, rate of `unsupported_inference`,
  optional UAR aggregation from judge fields.
- Inter-rater protocol when multiple judges score the same transcript.

## Honest scope

Until Phase B is specified and piloted, treat **v0** results as **single-turn**
unless explicitly rerun under a published dynamic protocol.
