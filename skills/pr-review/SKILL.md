---
name: pr-review
description: Review pull requests only when explicitly invoked. Inspect the change, compare it with project patterns and authoritative docs, preview any inline comments with their rationale, then wait for authorization before submitting the review.
---

# PR Review

## Activation and scope

Use this skill only when the user invokes `$pr-review` or explicitly asks to use the `pr-review` skill. Do not activate it from an ordinary PR review request alone.

Review the requested PR and prepare a GitHub review. Do not edit the PR branch, merge, push, or commit as part of this skill. Do not run tests unless the user asks; inspect existing CI results instead.

## Review workflow

1. **Inspect repository and PR conventions.** Locate the correct repository and read applicable `AGENTS.md`, `CLAUDE.md`, PR templates, `CODEOWNERS`, reviewer configuration, and relevant review guidance. Check the current PR state, base and head commits, changed files, existing reviews/comments, and CI checks. Review the latest head, not a stale local branch. Do not change repository configuration to fit the review.

2. **Understand the requested behavior.** Use the task description, acceptance criteria, and out-of-scope notes as the review contract. Identify the changed code's callers, data flow, persistence/API contracts, and related tests.

3. **Verify findings against evidence.** Compare the implementation with relevant patterns in the same codebase. For framework, database, GitHub, or other version-sensitive details, consult authoritative documentation and use primary sources. Browse when the fact may have changed, is niche, or needs a precise citation. Separate confirmed defects from conditional risks and state the condition that triggers each risk.

4. **Keep findings actionable.** Report behavior that can fail an acceptance criterion or cause a concrete reliability, data, security, performance, or integration issue. Avoid style-only suggestions and speculative concerns. Anchor each comment to a changed line. Keep one issue per comment, explain the failure condition and impact briefly, and include relevant links to official docs or local code patterns. Add a concise code sketch when it makes the fix clearer. Follow repository severity conventions; otherwise use a short title and a priority label only when useful.

## Mandatory preview before publication

Always show the user a review preview before posting any approval or comments. For every proposed inline comment, include:

- the target file and diff line;
- why the finding merits a comment, with evidence and any conditions;
- the exact formatted comment body, including relevant links and suggested code when useful.

Also state whether the review has no actionable findings. In that case, preview that the action will be approval only with no general PR comment. When findings exist, preview the exact general review body: `Mais detalhes nos comentários.`

Stop after the preview and wait for the user's explicit authorization to submit that exact review. An earlier request to review, approve, or comment does not waive this preview gate. If the PR head changes after preview, re-check the affected diff and show an updated preview before submitting. Never post unpreviewed or stale comments.

## Submission policy

Follow this user's review policy after authorization:

- **No actionable findings:** submit `APPROVE` with no body and no comments.
- **One or more findings:** submit `APPROVE` with the previewed inline comments and the exact general body `Mais detalhes nos comentários.` Do not use `REQUEST_CHANGES` unless the user explicitly changes this policy.

Re-check the PR state immediately before submission. If the PR is already merged or closed, do not submit a retroactive approval. Explain that approval can no longer affect the PR; post previewed comments only if they remain useful and the user authorized them. For inline review comments, use the current commit and current diff line/side fields from GitHub's supported API, not deprecated diff-position fields. Prefer one review submission containing the approved comments and review event.

After submission, verify the review state, commit, general body, and every comment's path, line, and text. If the result is uncertain, query GitHub before retrying to avoid duplicates.

## Final response

Keep the final report short. Link the submitted review or comments. State whether the PR was approved, whether comments were posted, and any state change that prevented approval. When no comments were needed, say approval only; do not add a general PR summary comment.
