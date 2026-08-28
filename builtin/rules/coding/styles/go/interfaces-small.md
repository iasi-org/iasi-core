# Small Go interfaces

## Metadata

| Field | Value |
|---|---|
| ID | coding.styles.go.interfaces-small |
| Description | Keeps interfaces minimal and behavior-focused. |
| Scope | coding/go |
| Level | should |
| Tags | coding; go; style; interfaces; api |

## Rule

Interfaces should contain the smallest set of methods required by their consumers. Large interfaces should be split when callers depend on only subsets of their behavior.

## Exceptions

A protocol that is intentionally exposed as one coherent interface may remain larger when its contract genuinely requires it.

## Rationale

Small interfaces are easier to implement, compose, test, and evolve.

## Sources

Effective Go: https://go.dev/doc/effective_go#interfaces

Go Style Decisions: https://google.github.io/styleguide/go/decisions

## Examples

Prefer `io.Reader`-sized behavioral contracts over service interfaces containing unrelated operations.
