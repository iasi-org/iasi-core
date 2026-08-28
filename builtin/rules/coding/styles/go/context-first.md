# Go context first

## Metadata

| Field | Value |
|---|---|
| ID | coding.styles.go.context-first |
| Description | Places context.Context first in function parameter lists. |
| Scope | coding/go |
| Level | must |
| Tags | coding; go; style; context; api |

## Rule

When a function or method accepts `context.Context`, it must be the first parameter and must be passed explicitly through the call chain.

## Exceptions

An externally imposed interface signature may require a different parameter order.

## Rationale

A consistent first-position context makes cancellation, deadlines, and request-scoped data visible and predictable.

## Sources

Go Code Review Comments: https://go.dev/wiki/CodeReviewComments

Go Style Decisions: https://google.github.io/styleguide/go/decisions

## Examples

```go
func Load(ctx context.Context, path string) (*Config, error) { ... }
```
