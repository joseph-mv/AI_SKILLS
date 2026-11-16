# Java

Use Javadoc for public and protected API. Package-private and private members get Javadoc only when they hide a rule a later editor needs. Do not add a Javadoc stub to every getter.

## Form

- Start with `/**` and put the summary in the first sentence. The summary stands alone.
- Use `@param`, `@return`, and `@throws` only when they add a constraint, a unit, or an error the signature does not name.
- `{@code}` is for a literal that would otherwise be read as prose. Do not wrap every identifier.
- Follow the project's HTML habits. If existing Javadoc is plain sentences, keep plain sentences.

```java
/**
 * Reserves stock for one order line.
 *
 * A discontinued SKU, or a quantity below one, throws
 * {@link ReservationException} before {@code inventory.reserve} is called.
 *
 * @throws ReservationException if the SKU is discontinued or the line
 *     quantity is less than one
 */
public Reservation reserve(OrderLine line) throws ReservationException {
    if (line.quantity() < 1 || catalog.isDiscontinued(line.sku())) {
        throw new ReservationException(line.sku());
    }
    return inventory.reserve(line);
}
```

Do not write `@param line the order line` when `line` is already an `OrderLine` and the method adds no further constraint on it.

A `//` comment inside the method is for a local decision that callers do not need in the generated docs. Do not restate the Javadoc there.
