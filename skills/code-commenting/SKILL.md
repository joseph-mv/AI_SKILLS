---
name: code-commenting
description: Writes, reviews, improves, and removes code comments and API documentation so comments explain why, not what. Use when asked to comment new code, review or improve comments, delete redundant comments, find outdated comments, document business logic, improve function or API docs, check comments during a refactor, or audit comment quality. Do not use for implementation tasks that do not ask for comments.
---

# Code commenting

Good code explains what it does. A comment explains why the code is the way it is. The goal is readability and maintainability, not a larger comment count.

Do not enforce a comment-to-code ratio. Do not add a comment to every function, field, or line. Skip a comment when the code and the existing documentation already say what a maintainer needs.

## Choose the workflow

Do only the task the user requested. Read [references/workflows.md](references/workflows.md) and follow that workflow.

1. Comment newly implemented code.
2. Review existing comments.
3. Improve poorly written comments.
4. Remove redundant comments.
5. Detect outdated comments.
6. Document complex business logic.
7. Improve function and API documentation.
8. Review comments while refactoring.
9. Audit comment quality.

If the request names more than one of these, do those and nothing else. A review does not become a rewrite unless the user asked for changes. An audit reports findings. It does not edit the repository unless the user asked to apply the findings.

## Before writing or changing a comment

1. Read the surrounding implementation, not only the line in front of you.
2. Read comments and documentation that already cover the same behavior.
3. Do not guess business requirements, threat models, or performance claims. Use only what the code, tests, and project documentation support.
4. Do not invent an explanation to fill a comment. If the intent is not established, ask for clarification and leave the code uncommented.
5. When the user allowed code changes, prefer a clearer name or structure over a comment that restates the code. When the user asked only for comments, do not change behavior or make unrelated edits.
6. Match the project's comment style, documentation tool, and language.
7. Re-read every comment you add or edit against the implementation.

## When to write a comment

Write a comment when it adds context the code cannot carry:

- Complex business logic, domain rules, and constraints.
- A non-obvious algorithm, including a complexity or mathematical reason when that is what makes the code correct.
- An important architectural decision or an unexpected implementation choice.
- Security-sensitive behavior and the decision behind it.
- A performance optimization whose reason is not obvious from the code.
- Concurrency, ordering, and synchronization constraints.
- A workaround for a framework, library, or language limitation.
- An important edge case or assumption.
- Non-obvious behavior of an external API.

## When not to write a comment

Do not write a comment that:

- Repeats the code or restates a function, type, or variable name.
- Explains an obvious statement, or narrates every line.
- Adds a decorative banner or a redundant section header.
- Documents a simple variable that the name already explains.
- Exists only to raise comment coverage.
- Duplicates documentation already next to the code or in the project docs.

This comment restates the statement. Remove it:

```javascript
// Increment the counter
counter++;
```

This comment matches the control flow. The cold-start status and the single retry are not visible from the condition alone:

```javascript
// The payments API returns 503 for a few seconds after a cold start.
// One retry covers that window. A later 503 is returned to the caller.
if (response.status === 503 && attempt === 0) {
  return charge(request, attempt + 1);
}
```

Do not attach that explanation to a bare `counter++`, or to any code that does not retry once on HTTP 503.

## Match the comment to the risk

- Business-critical code: state the domain rule the code enforces. Name the source only when it is in the repository or the user supplied it.
- Security-sensitive code: state the decision and the property it protects. Do not invent a threat the code does not address.
- Algorithm-heavy code: state the approach, a complexity reason, or an invariant when a reader cannot recover it from the implementation.
- Public APIs and functions other modules call: document a contract the caller cannot learn from the name alone. Use the language's documentation format.
- UI code: do not comment obvious rendering. Comment a non-obvious interaction, accessibility rule, or platform constraint.
- Tests: comment a non-obvious scenario or unusual setup. Do not comment an assertion the test name already states.

Skip documentation on trivial private details. A private helper whose name and body are obvious does not need a docstring, Javadoc comment, or XML comment.

## Language conventions

Use the language's own documentation format. Do not force one style onto every language. If the project already uses a documentation tool, follow that tool.

Open only the reference for the language you are editing:

- JavaScript and TypeScript: [references/javascript-typescript.md](references/javascript-typescript.md)
- Python: [references/python.md](references/python.md)
- Java: [references/java.md](references/java.md)
- C#: [references/csharp.md](references/csharp.md)
- Go: [references/go.md](references/go.md)
- Rust: [references/rust.md](references/rust.md)
- Other languages: [references/other-languages.md](references/other-languages.md)

For comments that should stay or go, see [references/examples.md](references/examples.md).

## Keep comments true when code changes

When you modify implementation:

- Read the comments on the changed logic and on the callers you affect.
- Update an explanation the change makes incomplete or wrong.
- Remove a comment that is now redundant.
- Keep a comment that still carries business or design context.
- Do not delete useful context only to reduce the comment count.
- Do not leave a comment that contradicts the code.

## Finish

Check every comment you added or chose to leave. For a review or an audit, apply these same checks using [references/checklist.md](references/checklist.md).

1. It adds information the code does not already state.
2. Where why is the point, it explains why.
3. The explanation is true of this implementation.
4. It is concise.
5. It sits next to the code it describes.
6. It follows the language's documentation form and the project's existing tool.
7. It is not outdated.
8. Another developer would benefit from reading it.

If a comment fails, improve it or remove it. Do not replace it with a different unsupported explanation.
