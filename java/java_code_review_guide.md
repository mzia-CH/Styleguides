# Java Code Review Guide

## 1. Developer Actions Prior to Code Commit/Review

Before committing code or requesting a review, ensure the following:

### Code Quality & Readability
- Code is formatted and tidy (proper indentation, reasonable line length, no commented-out code, no spelling mistakes).
- Javadoc is included where appropriate.
- Unused imports are removed.
- Warnings from the IDE are resolved.
- Any TODO comments are removed.
- No leftover stubs or test routines.
- No hardcoded development-only values.
- Performance and security considerations have been made.
- The code follows established coding standards.

### Functionality & Testing
- Code compiles successfully.
- Code has been developer-tested and includes unit tests.
- Proper use of exceptions and logging is implemented.
- Possible NullPointerExceptions (NPEs) have been considered and handled.
- Corner cases and workarounds for framework limitations are documented.
- The code correctly releases resources (HTTP connections, DB connections, files, etc.).
- Code does not depend on bugs in external frameworks that might be fixed later.

### Maintainability & Reusability
- Can any code be replaced by calls to external reusable components or library functions?
- Thread safety and possible deadlocks have been reviewed.
- Code follows best practices for scalability and maintainability.
- Commit messages follow the standard format.

## 2. Code Review Severity Levels

| Issue Type                 | Severity Level |
|----------------------------|---------------|
| Naming Conventions & Coding Style  | Low           |
| Control Structures & Logical Issues | Medium/High  |
| Redundant Code             | High          |
| Performance Issues         | High          |
| Security Issues            | High          |
| Scalability Issues         | High          |
| Functional Issues          | High          |
| Error Handling             | High          |
| Reusability                | Medium        |

## 3. Code Review Checklist

### 3.1 General Code Quality
- Method and class names are simple and self-explanatory.
- Class, variable, and method modifiers are correctly assigned.
- Class and method sizes are appropriate.
- Complex algorithms are well-documented with references.
- Units of measurement for numeric values are documented.
- JSPs do not contain business logic.
- Repetitive code has been refactored appropriately.
- Code aligns with existing architecture and design patterns.
- Objects not returned from methods are not modified unless necessary.

### 3.2 Testing & Validation
- Unit tests cover each code path, including error conditions and invalid parameters.
- Standard algorithms are tested against expected results.
- Edge cases and corner cases are explicitly tested.
- Code fixes have corresponding unit tests, and issue numbers are referenced in documentation.
- Arrays and collections are checked for index bounds before access.
- Code does not reimplement existing functionality available in public frameworks.

### 3.3 Error Handling & Exceptions
- Fast-fail approach: Invalid parameters are handled early.
- NullPointerExceptions are explicitly handled.
- General error handlers clean up resources properly.
- Avoid using `RuntimeException` and sub-classes unless necessary.
- Use custom Exception sub-classes for specific error conditions and document their usage.
- Do not throw generic `Exception`; handle exceptions appropriately.
- Do not swallow exceptions (e.g., `catch (Exception ignored) {}`). Always log exceptions.
- Avoid returning `null` from methods unless necessary.
- (JDK 7+) Use try-with-resources where applicable. (JDK < 7) Ensure resources are explicitly closed.

### 3.4 Thread Safety
- Static (global) variables are properly synchronised.
- Objects accessed by multiple threads use appropriate locks.
- Locks are acquired and released in the correct order to prevent deadlocks, including error-handling scenarios.

### 3.5 Performance Considerations
- Objects are duplicated only when necessary (consider implementing `Clone` with deep/shallow copy as required).
- Avoid busy-wait loops (`while(true) { ... sleep(10); ... }`) and use proper synchronization mechanisms.
- Large objects are not kept in memory unnecessarily.
- Avoid using `String` for handling large documents; prefer efficient alternatives (e.g., `StringBuilder`, streaming APIs).
- Debugging code is removed from production (e.g., no `System.out.println();`).
- Optimization that makes code harder to read should only be implemented if a profiler or other tool has indicated that the routine stands to gain from optimization. These kinds of optimizations should be well documented and code that performs the same task should be preserved.
