# Python

Public modules, classes, and functions use PEP 257 docstrings. Follow the project's existing style when it already uses Google, NumPy, or Sphinx sections. Do not introduce a second style in the same package.

## Form

- Use triple double quotes.
- A one-line docstring is a single line, including the closing quotes, and only when one sentence is enough.
- A longer docstring has a summary line, a blank line, then the detail.
- Write the summary as an imperative phrase ending in a period: "Return the discounted subtotal." Do not write "Returns the discounted subtotal."
- Put the closing quotes on their own line for a multi-line docstring.

## What to include

Include a docstring when it states a contract the signature does not:

- Which values are eligible.
- What is included or excluded.
- Exceptions that are part of the contract.
- Side effects a caller must expect.

Skip a docstring on a trivial private helper. A leading underscore does not by itself forbid a docstring; the test is whether the helper hides a rule. Do not add an `Args` section that only repeats parameter names.

```python
def apply_tier_discount(amount: Decimal, tier: str) -> Decimal:
    """Return amount after the tier discount.

    Platinum takes 15 percent off, gold takes 10 percent off, and any
    other tier returns amount unchanged.
    """
    if tier not in {"gold", "platinum"}:
        return amount
    rate = Decimal("0.15") if tier == "platinum" else Decimal("0.10")
    return amount * (Decimal("1") - rate)
```

A module docstring should say what the module is for when the package layout does not. Do not restate the filename.

Use a `#` comment inside a function for a local decision. Do not move that decision into the docstring unless callers need it.
