# Commenting workflows

Do the workflow the user asked for. Do not start a second workflow because it would also be useful.

## Comment newly implemented code

Use when the user asks for comments on code that was just written.

1. Read the new code and the code it calls.
2. Comment only the spots listed in `SKILL.md` under "When to write a comment."
3. Add API documentation only for a contract the signature does not already state.
4. Run the finishing checks.

Out of scope: redesigning the implementation, adding features, or commenting unchanged code the user did not include.

Example: "Comment the new payment retry. Explain only what the code itself does not show."

## Review existing comments

Use when the user asks for a review of comments, not an edit.

1. Read each comment against the current code.
2. Report comments that are wrong, redundant, or missing a why the code needs.
3. Quote the comment and name the file. Say whether to keep, change, or remove it, and why.
4. Do not edit unless the user asked you to apply the review.

Out of scope: rewriting comments in place, changing code, or proposing new features.

Example: "Review the comments in `billing/`. Do not change files."

## Improve poorly written comments

Use when the user asks to improve comments that are vague, restated, or misleading.

1. Replace a restatement with the why, or remove it if there is no why.
2. Keep a comment whose facts are still correct.
3. Do not add a fact the implementation does not support.

Out of scope: behavior changes, and comments outside the requested area.

Example: "Improve the comments in `apply_tier_discount`. Keep the business rule, and remove anything that repeats the code."

## Remove redundant comments

Use when the user asks to delete comments that add nothing.

1. Remove comments that repeat the code, the name, or documentation already present.
2. Leave comments that still carry a rule, constraint, or decision.
3. Do not delete a comment only because the file has many comments.

Out of scope: rewriting the remaining comments, unless one you touched is now false, and any functional edit.

Example: "Remove redundant comments in `src/ui`. Leave comments that explain a platform constraint."

## Detect outdated comments

Use when the user asks to find comments that no longer match the code.

1. Compare each comment with the implementation it describes.
2. Report the contradiction. Cite the comment and the code that makes it false.
3. Do not change files unless the user asked to update them.
4. If they did, update the comment to the current behavior or remove it when it no longer adds anything. Do not invent the original intent.

Out of scope: a general code review, and comments that are merely stylistically weak. Those belong to the improve workflow.

Example: "Find outdated comments in `auth/`. List them. Do not edit yet."

## Document complex business logic

Use when the user asks to document domain rules in the code.

1. Find the rule in the implementation, tests, or documentation the user pointed at.
2. Write the constraint the code enforces. Name a source only when you can point at it.
3. Ask when the code can support more than one interpretation.

Out of scope: inventing policy, and changing the rule so the comment is easier to write.

Example: "Document the discount rule in `apply_tier_discount`. Use only what the function does."

## Improve function and API documentation

Use when the user asks for docstrings, Javadoc, XML comments, Go docs, rustdoc, JSDoc, or TSDoc.

1. Open the language reference for the file you are editing.
2. Document the contract a caller cannot learn from the signature: units, side effects, errors, ordering, and invariants.
3. Skip trivial private helpers.
4. Follow the project's existing documentation tool when it differs from the language default.

Out of scope: a comment on every internal function, and prose that repeats the parameter names.

Example: "Add docs to the public methods in `InvoiceService`. Skip private helpers."

## Review comments while refactoring

Use when a refactor is in progress or the user asks whether the comments survived a refactor.

1. Read the comments on every changed region and on callers whose assumptions changed.
2. Update a comment the refactor made false.
3. Remove a comment the refactor made redundant.
4. Preserve a comment whose business or design context is still true.
5. Do not expand the refactor into unrelated cleanup.

Out of scope: a repository-wide comment audit, unless the user asked for one.

Example: "I split charge into two functions. Update the comments the split made wrong, and do not change the new control flow."

## Audit comment quality

Use when the user asks for an audit, a pass over a repository, or a comment-quality report.

1. Sample the areas the user named. If they named the whole repository, prioritize public APIs, business rules, security, concurrency, and code with dense comments.
2. Apply the checks in [checklist.md](checklist.md).
3. Report findings first. Group them as wrong, redundant, or missing-and-needed.
4. Do not edit unless the user asked to apply the audit.

Out of scope: enforcing a comment quota, and commenting every function so the audit looks complete.

Example: "Audit comment quality under `src/`. Report wrong, redundant, and missing comments. Do not edit."
