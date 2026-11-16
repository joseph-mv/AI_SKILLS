# Comment examples

Each good comment is true of the code beside it. A comment that could describe some other program is not an improvement.

## A comment that restates the code

Remove a comment that only names the next statement.

```javascript
// Increment the counter
counter++;
```

`counter++` already says what happens. There is no why to record, so the comment goes away. Do not replace it with a story about retries, limits, or business rules unless that story is what this statement does.

## A business rule

The rates are visible in `apply_tier_discount`. The reason tax and shipping are absent from that call is not.

```python
def checkout_total(
    merchandise: Decimal, tax: Decimal, shipping: Decimal, tier: str
) -> Decimal:
    # Tier rates apply to merchandise only. Tax and shipping stay at the
    # amounts already calculated for this order.
    return apply_tier_discount(merchandise, tier) + tax + shipping
```

`apply_tier_discount` takes one amount and returns 15 percent off for platinum, 10 percent off for gold, and the same amount for any other tier. The comment above is valid because this caller passes merchandise and adds tax and shipping afterward.

This docstring repeats the names and drops the rule:

```python
def apply_tier_discount(subtotal: Decimal, tier: str) -> Decimal:
    """Applies the tier discount to the subtotal.

    Args:
        subtotal: The subtotal.
        tier: The tier.
    """
```

Write a parameter section only when the project already uses one and the text adds a constraint.

## A security decision

The empty-account branch still runs scrypt. The comment says why that digest is computed and then discarded.

```python
import hashlib
import hmac


def password_matches(stored_hash: str, candidate: str) -> bool:
    # An unknown account is stored as an empty string. Hashing the candidate
    # anyway keeps that branch on the same scrypt cost as a real account.
    # The digest is discarded. Only a stored hash is compared.
    if stored_hash == "":
        hashlib.scrypt(
            candidate.encode(), salt=b"timing-pad", n=2**14, r=8, p=1
        )
        return False
    digest = hashlib.scrypt(
        candidate.encode(), salt=b"timing-pad", n=2**14, r=8, p=1
    )
    return hmac.compare_digest(stored_hash, digest.hex())
```

Do not write "hash the password" above the `scrypt` call. That repeats the call and drops the reason for hashing the empty-account branch. Do not claim this function salts per user: the salt in this snippet is fixed.

This example illustrates the comment, not a complete password store. A production store needs a unique salt and stored scrypt parameters. The empty-account branch and the real-account branch are not fully equal in time: only the real account calls `compare_digest`. The comment does not claim that they are.

## An obvious UI comment

Delete a comment that narrates the render.

```tsx
// Return a button
return <button type="submit">Save</button>;
```

Keep a comment when the markup exists for a platform rule the element does not state:

```tsx
// role="status" announces saveError when it changes, without moving focus
// to this paragraph.
<p role="status">{saveError}</p>
```

## A non-obvious test

The test name already says the first deadline is kept. The comment says why a later call does not replace it.

```python
from datetime import datetime, timedelta, timezone


def test_duplicate_delivery_keeps_the_first_deadline():
    # The hold key is the event id. setdefault keeps the deadline computed
    # from the first delivery when the same id arrives again.
    holds = {}
    first = datetime(2026, 1, 1, tzinfo=timezone.utc)
    later = datetime(2026, 1, 1, 0, 5, tzinfo=timezone.utc)

    def place(event_id: str, at: datetime) -> None:
        holds.setdefault(event_id, at + timedelta(seconds=600))

    place("evt-1", first)
    place("evt-1", later)
    assert holds["evt-1"] == first + timedelta(seconds=600)
```

Do not add "assert the deadline" above the assertion. The test name already says what is checked. The comment is there because `setdefault` is the reason a later delivery does not move the deadline.
