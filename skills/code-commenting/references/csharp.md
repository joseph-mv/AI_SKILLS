# C#

Use XML documentation comments on public APIs. Document an internal or private member only when it carries a rule the signature does not. Match the project's existing tags. Do not add an empty `<summary>` so that a documentation generator stays quiet.

## Form

- Start with `///`.
- `<summary>` is one or two sentences a caller can use without reading the body.
- Add `<param>`, `<returns>`, or `<exception>` only for a constraint, a unit, or an error condition.
- Use `<see cref="Type"/>` for a real type a reader should open. Do not wrap ordinary words in `cref`.

```csharp
/// <summary>
/// Reserves stock for one order line.
/// A discontinued SKU, or a quantity below one, throws before the inventory reservation is called.
/// </summary>
/// <exception cref="ReservationException">
/// The SKU is discontinued, or <paramref name="line"/> has a quantity below one.
/// </exception>
public Reservation Reserve(OrderLine line)
{
    if (line.Quantity < 1 || _catalog.IsDiscontinued(line.Sku))
    {
        throw new ReservationException(line.Sku);
    }

    return _inventory.Reserve(line);
}
```

Do not add `<param name="line">The order line.</param>`. The type and the name already say that.

Use a `//` comment inside the method for a local decision that callers do not need in the generated docs.
