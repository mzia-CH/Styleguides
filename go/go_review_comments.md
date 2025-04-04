

## Go Coding Review Comments

This document outlines key practices for writing clean, efficient, and idiomatic Go code. It is based on the comprehensive [Go Code Review Comments guide](https://go.dev/wiki/CodeReviewComments).

### Code Formatting and Style

**Gofmt and Imports**
- Use `gofmt` or `goimports` to automatically format your code.
- Organise imports in groups: standard library first, then third-party packages.

**Naming Conventions**
- Use MixedCaps for names. Avoid underscores.
- Treat acronyms as words in names (e.g., `urlPony` or `URLPony`, not `UrlPony`).
- For unexported constants, use `maxLength` not `MaxLength` or `MAX_LENGTH`.

**Comments**
- Write full sentences for declarations, starting with the name of the thing described.
- Example: `// Request represents a request to run a command.`

### Code Structure and Design

**Error Handling**
- Return errors explicitly. Avoid in-band errors (like returning -1 for failure).
- Handle errors immediately:

```go
if err != nil {
    // error handling
    return // or continue, etc.
}
// normal code
```

**Interfaces**
- Define interfaces in the package that uses them, not the one that implements them.
- Don't define interfaces prematurely; wait for concrete use cases.

**Goroutines**
- Ensure clear goroutine lifetimes to prevent leaks and race conditions.
- Document when and why goroutines exit if it's not obvious.

### Best Practices

**Context Usage**
- Pass `context.Context` as the first parameter in functions that use it.
- Don't add Context to struct types; pass it in method parameters.

**Slices**
- Prefer `var t []string` over `t := []string{}` for empty slices.

**Crypto**
- Use `crypto/rand` for generating keys, not `math/rand`.

**Testing**
- Include examples in new packages to demonstrate usage.
- Use testable `Example()` functions.

### Common Pitfalls to Avoid

- Don't use `panic` for normal error handling.
- Avoid renaming imports except to prevent name collisions.
- Don't use `import .` except in specific test scenarios.
- Avoid copying structs from other packages to prevent unexpected aliasing.

### Additional Topics

**Naked Returns**
- Avoid naked returns in longer or more complex functions, as they can harm readability.

**Package Comments**
- Add a package comment for each package, placed before the package clause.
- For "main" packages, the comment should describe the program's purpose.

**Package Names**
- Choose package names that are concise, clear, and avoid redundancy.
- Avoid generic names like "util" or "common".

**Pass Values**
- Don't pass pointers as function arguments just to save a few bytes.
- If a function only needs a small part of a large struct, consider passing just that part.

**Synchronous Functions**
- Prefer synchronous functions over asynchronous ones when performance is not critical.

**Useful Test Failures**
- Write test failures that are useful for debugging.
- Include relevant information in error messages.

**Variable Names**
- Use short variable names for short scopes, and longer names for broader scopes.
- The larger the scope, the more descriptive the name should be.
