# Other languages

Follow the documentation tool the repository already uses. The notes below are the usual form when the project has not chosen one. They are not a reason to replace an existing style.

- Kotlin: KDoc (`/** */`) on public declarations. The first sentence is the summary. Use `@param`, `@return`, and `@throws` only for a constraint the signature does not state.
- Ruby: RDoc, in comments above the method or in a block immediately after the `def` line if that is the project style. Document the contract, not a restatement of the method name.
- PHP: PHPDoc (`/** */`) where the project generates API docs. In code that already has PHP types, do not repeat those types in `@param` unless the tag adds a constraint. Follow the project's PHPDoc dialect.
- Swift: `///` (or `/** */`) on public declarations, in the DocC form the project uses. The summary is the first sentence. Add a parameter paragraph only for a constraint.
- C and C++: follow the project's tool. Doxygen is the common choice when a tool is in use. If the project uses plain comments, keep plain comments. Document ownership, lifetime, and locking when the signature cannot say them. Do not add a Doxygen stub to every function in a project that does not use Doxygen.

For every language, a comment still has to add a why or a contract. A documentation block that repeats the declaration fails the same checks as a one-line restatement.
