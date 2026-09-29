---
name: completion-gate
description: Apply a bounded completion audit to every implementation or change before declaring it done. Verify the requested behavior in its actual system context, fix blockers, and report validation and status.
---

# Completion Gate

Treat "done" as sufficient evidence that the requested change works safely in its actual system context. Do not optimize for theoretical perfection.

## 1. Anchor the task

Before declaring completion, identify:

- the requested behavior and acceptance criteria;
- the deliverable type and evidence level required;
- the code, documents, and contracts directly affected;
- relevant callers, dependencies, tests, configuration, and data flows.

If acceptance criteria are implicit, infer them from the request and existing system behavior.

Do not expand the task into unrelated cleanup or redesign.

### Match verification to the deliverable

Use evidence appropriate to the requested stage; passing one level does not imply the next:

- **Document/specification:** check source authority, traceability, cross-document consistency, completeness, links, and acceptance criteria. Runtime proof is not required unless requested.
- **Schema/contract:** distinguish JSON syntax and schema validity from instance behavior, cross-record semantics, and adapter/runtime behavior. Verify only the layers in scope and report the rest as unverified.
- **Implementation/integration:** verify behavior in the relevant code path and system context with permitted checks.
- **Runtime/production:** require the requested observed evidence, such as POC results, telemetry, cost, restore, or alert behavior.

Missing downstream evidence is not a blocker for an earlier-stage deliverable unless its acceptance criteria explicitly require it.

For multi-turn work, keep proposed, approved, implemented, and observed states distinct. Record what an approval covers; approval of a document or estimate does not authorize external changes. Preserve explicit authorization, and satisfy any repository review gate before the exact mutation.

## 2. Implement

Make the smallest coherent change that satisfies the task and existing project conventions.

Prefer repository-specific contracts and patterns over generic best practices.

## 3. Run one completion audit

After implementation, perform one bounded review of the resulting change.

Check only where relevant:

- correctness and meaningful edge cases;
- callers, dependencies, interfaces, state, configuration, and regressions;
- affected security boundaries, authorization, validation, secrets, and untrusted input;
- performance or resource impact when the changed path can materially affect scale, latency, I/O, concurrency, or memory;
- migrations, retries, timeouts, failure handling, and operational behavior when applicable;
- available tests, build, type checking, linting, or other project validation.

Follow the active instruction hierarchy and the user's authorization when choosing validations. Run only checks permitted for the task, and report relevant checks that were not run as unverified.

A concern must have a concrete failure condition or plausible affected path. Do not create work from purely hypothetical improvements.

## 4. Classify findings

A finding is a **blocker** when it can materially cause:

- failure of an acceptance criterion;
- incorrect behavior or regression;
- broken integration or contract;
- security vulnerability;
- data loss or corruption;
- material reliability or performance regression;
- failure of relevant validation.

Fix blockers before declaring the task done.

A **non-blocking improvement** is something that could make the implementation cleaner, more general, faster, or easier to maintain without being necessary for the requested behavior or materially reducing current risk.

Do not continue implementation for non-blocking improvements unless the task explicitly requires them.

## 5. Revalidate without reopening review

After fixing a blocker, re-run the checks affected by that fix.

Do not restart a broad critique of the implementation after every correction.

Run another broad audit only if the fix materially changed the architecture, contracts, or scope. Never perform more than two broad audits for the same task.

## 6. Stop condition

Declare `DONE` when:

- the requested behavior is implemented;
- relevant acceptance criteria are satisfied;
- relevant permitted validation passes;
- no known blockers remain.

Declare `PARTIAL` or `BLOCKED` instead when a material issue remains because of missing information, unavailable environment, external dependency, or an unresolved blocker.

Unavailable or disallowed validation must be reported as unverified; it must not silently be treated as passing.

Non-blocking improvements are not a reason to delay `DONE`.

## Final response

Lead with a one-sentence conclusion that directly answers the user's original request and says what is now established or ready. Do not make the user infer the outcome from the status or validation details.

Keep the completion report concise:

- conclusion: the direct answer or outcome;
- status: `DONE`, `PARTIAL`, or `BLOCKED`;
- what materially changed;
- validation performed and its result;
- unresolved blockers or known material risks, if any.

Optionally mention at most three directly relevant non-blocking improvements. Do not investigate or elaborate on them unless requested.
