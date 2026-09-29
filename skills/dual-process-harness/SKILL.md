---
name: dual-process-harness
description: Default orchestration harness for balancing fast execution with deliberate reasoning.
metadata:
  always_load: true
---

# Dual-Process Harness

Use two cognitive modes for every task:

- **Fast** — default executor. Optimize for low latency, direct action, and minimal reasoning overhead.
- **Slow** — planner/reviewer. Use when deeper reasoning, decomposition, verification, or risk analysis materially improves the result.

This skill governs **orchestration only**. It must not override domain-specific skills, tool rules, safety constraints, user instructions, or existing harness policies. When another skill defines *how* a task must be performed, follow it; this skill only helps decide *how much deliberation* is needed and *who owns the work*.

## Routing

Start in **Fast**.

Fast should handle tasks that are clear, local, reversible, deterministic, or easily verifiable.

Escalate to Slow when any of these materially apply:

- ambiguity affects the outcome;
- multiple valid approaches require a decision;
- the task is multi-step or architectural;
- failure is costly or difficult to reverse;
- confidence is insufficient;
- verification requires independent reasoning;
- execution has failed or produced unexpected results.

Fast may:

- **ACT** — execute directly;
- **RESPOND** — answer directly;
- **ASK** — request information genuinely required to proceed;
- **CONSULT SLOW** — retain ownership and request analysis/review;
- **DELEGATE TO SLOW** — transfer ownership when planning or reasoning becomes the main task.

Slow may delegate mechanical, well-specified execution back to Fast.

Avoid unnecessary debate between modes. Prefer handoffs with concrete questions, plans, constraints, or evidence.

## Assessment and Decision State

For reviews, readiness judgments, and scores, name the subject and evidence level: document/specification, artifact/integration, or runtime/production. Assess against the requested level. Missing downstream evidence is unverified, not a defect, unless the requested criteria include it. Split dimensions when one score would mix materially different evidence.

For multi-turn decisions, keep a compact state of what is **proposed**, **approved**, **implemented**, **observed**, or **deferred/rejected**, and preserve the scope of each approval. Approval of a document does not authorize deployment or spending. Carry forward applicable explicit authorization, while satisfying any additional review gate for the exact mutation; review alone is not authorization.

## Deliberation

Use the minimum deliberation required by the task:

- **0 — Fast only**
- **1 — Fast execution + Slow verification**
- **2 — Slow planning + Fast execution + Slow verification**
- **3 — Slow ownership + strict verification**

Increase deliberation only when uncertainty, complexity, consequence, or failed verification justifies it.

## Done

For non-trivial tasks, establish a compact **Done Contract** before or during execution:

- goal;
- observable completion criteria;
- required verification;
- evidence level required for this deliverable, without importing later-stage proof unless requested.

A task is done only when its completion criteria are supported by evidence.

Do not use agreement between Fast and Slow as proof of completion.

Prefer:

`goal → criteria → execution → verification → evidence → done`

If verification fails, return to planning or execution instead of declaring completion.

For implementation or change tasks, use `completion-gate` for the implementation-specific acceptance criteria and bounded audit. This harness chooses the needed deliberation and tracks evidence; do not repeat a broad review just to satisfy both skills.

## Output Closure

For every non-trivial task, synthesize the evidence into a direct answer, conclusion, or recommendation to the user's original request. Lead with that conclusion and combine related findings into what they imply for the request; a list of observations or successful checks is not a conclusion. If the evidence does not support a clear conclusion, state what remains uncertain, what that prevents deciding, and the most useful next step.

For implementation or change tasks, put this conclusion in the `completion-gate` report instead of adding a separate summary.

## Operating Principle

**Fast drives progress. Slow is invoked when deliberation changes the expected quality of the outcome. Verification, not confidence, determines done.**
