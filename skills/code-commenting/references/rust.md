# Rust

Use rustdoc comments. `///` documents the next item. `//!` documents the enclosing module or crate. Do not document every private function. Document a private item when it holds an invariant, an unsafe obligation, or a domain rule.

## Form

- The first line is a summary that stands alone.
- Add a section only when it applies: `# Errors`, `# Panics`, `# Safety`, `# Examples`.
- `# Safety` is required in spirit on `unsafe` functions: state what the caller must guarantee. Do not write a safety section that says "this is safe."
- Prefer types and `Result` over a comment that only says an error might happen. Use `# Errors` when the error variants need a rule the type does not state.
- Examples in rustdoc should compile when the project runs doctests. Do not add a fenced example that would fail `cargo test` unless you mark it `ignore` or `no_run` for a reason you state.

```rust
/// Reserves stock for one order line.
///
/// A discontinued SKU returns [`ReservationError::Discontinued`] and does
/// not call [`inventory::reserve`].
///
/// # Errors
///
/// Returns [`ReservationError::EmptyLine`] when `line.quantity` is zero.
pub fn reserve(line: &OrderLine) -> Result<Reservation, ReservationError> {
    if line.quantity == 0 {
        return Err(ReservationError::EmptyLine);
    }
    if catalog::is_discontinued(line.sku) {
        return Err(ReservationError::Discontinued);
    }
    inventory::reserve(line)
}
```

Do not write `/// Reserves a line.` and a `# Parameters` section that repeats `line`. Use a `//` comment inside the function for a local decision that is not part of the crate's public contract.
