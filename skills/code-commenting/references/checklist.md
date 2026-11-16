# Comment checklist

These are the same checks as the finish section of `SKILL.md`. A review or an audit uses them to classify a comment. They are not a second, stricter standard.

For each comment you added, edited, or included in a review, answer:

1. Does it add information the code does not already state?
2. Where the point is why, does it explain why?
3. Is that explanation true of this implementation?
4. Is it concise?
5. Is it next to the code it describes?
6. Does it follow the language's documentation form and the project's existing tool?
7. Is it free of outdated information?
8. Would another developer benefit from reading it?

A comment that fails is improved or removed. Do not keep it and add a second comment that contradicts it.

## How to classify a finding

- Wrong: the comment disagrees with the code, or states a rule, threat, or cost the code does not implement. This includes a comment left behind by a refactor.
- Redundant: the comment repeats the code, the declaration name, or documentation already present. Removing it does not drop a rule or a decision.
- Missing: a reader cannot recover a domain rule, security decision, invariant, or external quirk from the code, and the user asked for that gap to be documented. Do not list a missing comment for obvious code.

When the user asked for a report rather than edits, use this shape:

```text
src/billing/discount.py:12  Redundant
  "Applies the tier discount to the subtotal" repeats the function name.
  The merchandise-only rule is not stated. Ask before adding it if the
  function body is not enough to settle the rule.
```

Do not score the repository by comment count, coverage, or a ratio of comments to lines.
