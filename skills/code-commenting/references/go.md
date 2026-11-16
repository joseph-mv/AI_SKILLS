# Go

Go doc comments are ordinary comments immediately above the declaration, with no blank line between them. A complete sentence starts with the name being declared. `godoc` and `pkgsite` use that sentence as the summary.

Document an exported function, type, or the package comment when a reader of the docs needs a contract. Do not comment an unexported helper whose name and body are obvious. An unexported function still gets a comment when it hides a concurrency rule, a protocol quirk, or a domain constraint.

## Form

- `Package payments ...` is the package comment, placed before `package`.
- `Charge retries ...` documents `func Charge`.
- Start with the declared name so the sentence reads correctly in the docs index.
- Do not use `@param` tags. Put constraints in sentences.
- A bug note uses `BUG(name):` only when the project already marks bugs that way.

```go
// Charge submits one payment and retries once when the provider returns
// HTTP 503. A later 503, and any 402, is returned to the caller.
func Charge(ctx context.Context, req Request) (Result, error) {
    resp, err := provider.Charge(ctx, req)
    if err != nil {
        return Result{}, err
    }
    if resp.StatusCode == http.StatusServiceUnavailable {
        // The provider returns 503 for a few seconds after a cold start.
        // This second call is the only retry. Its status and error are returned as-is.
        return provider.Charge(ctx, req)
    }
    return resp, nil
}
```

The second `provider.Charge` is the one retry. The comment is on that call because the status check alone does not say that a second 503 is not retried. The doc comment states the contract. The line comment states the local decision. Do not copy one into the other word for word.

Do not write `// Charge charges the request` above `func Charge`.
