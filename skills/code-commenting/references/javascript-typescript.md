# JavaScript and TypeScript

Use the documentation form the project already uses. Prefer JSDoc for JavaScript. Use TSDoc only when the project already uses TSDoc tags or emits docs with a TSDoc tool. Do not mix both styles in one file.

## What to document

Document an exported function, class, or type when the contract is not the signature:

- Units, ranges, and sentinels.
- What is mutated, returned, or thrown.
- Ordering, retries, and compatibility constraints.
- A type-level quirk TypeScript does not express, such as a value that is present only after a specific state.

In TypeScript, do not repeat parameter types in `@param`. The type is already declared. Write `@param` only to add a constraint.

Skip a private function whose name and body are obvious. Skip a comment that restates a type.

## JSDoc

```javascript
/**
 * Charges the card once, then retries once if the provider returns 503.
 *
 * A later 503 is returned to the caller. This does not retry a 402.
 *
 * @param {ChargeRequest} request
 * @param {number} attempt Zero on the first call. Callers outside this module pass 0.
 * @returns {Promise<ChargeResult>}
 */
async function charge(request, attempt = 0) {
  const response = await provider.charge(request);
  if (response.status === 503 && attempt === 0) {
    return charge(request, attempt + 1);
  }
  return response;
}
```

`@param {ChargeRequest} request` adds nothing when a type is already in scope and the name is clear. `@param` earns its place on `attempt` because the legal value is a calling convention, not a shape.

## TSDoc

Use TSDoc when the project already does. TSDoc does not use type expressions inside `{ }`.

```typescript
/**
 * Charges the card once, then retries once if the provider returns 503.
 *
 * A later 503 is returned to the caller. This does not retry a 402.
 *
 * @param attempt - Zero on the first call. Callers outside this module pass 0.
 */
export async function charge(request: ChargeRequest, attempt = 0): Promise<ChargeResult> {
  const response = await provider.charge(request);
  if (response.status === 503 && attempt === 0) {
    return charge(request, attempt + 1);
  }
  return response;
}
```

Do not write `@param request - The request` under a typed `request` parameter.

## Line comments

Use a `//` comment for a local constraint that is not part of the public contract. Keep the block comment (`/** */`) for the contract. Do not add a banner such as `// ---- helpers ----`.
