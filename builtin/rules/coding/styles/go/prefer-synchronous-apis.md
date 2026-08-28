# Prefer synchronous Go APIs

## Metadata

| Field | Value |
|---|---|
| ID | coding.styles.go.prefer-synchronous-apis |
| Description | Prefers synchronous functions and lets callers add concurrency. |
| Scope | coding/go |
| Level | should |
| Tags | coding; go; style; concurrency; api |

## Rule

Functions should normally return their result synchronously rather than creating hidden background goroutines or callback-based asynchronous behavior. Callers may introduce concurrency explicitly when they need it.

## Exceptions

APIs whose purpose is inherently asynchronous or streaming may expose asynchronous behavior.

## Rationale

Synchronous functions are easier to reason about, test, compose, and cancel without leaking goroutines.

## Sources

Go Code Review Comments: https://go.dev/wiki/CodeReviewComments

## Examples

Prefer `result, err := Load()` and let the caller use `go Load()` when concurrency is needed.
