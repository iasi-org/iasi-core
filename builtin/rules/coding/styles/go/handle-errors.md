# Handle Go errors

## Metadata

| Field | Value |
|---|---|
| ID | coding.styles.go.handle-errors |
| Description | Requires every returned error to be handled deliberately. |
| Scope | coding/go |
| Level | must |
| Tags | coding; go; style; errors |

## Rule

A returned error must be handled, returned, or explicitly justified when ignored. Errors must not be silently discarded with `_` as a convenience.

## Exceptions

An error documented as impossible or irrelevant may be discarded only with a comment explaining why it is safe.

## Rationale

Explicit error handling is fundamental to Go control flow and prevents silent failure.

## Sources

Go Code Review Comments: https://go.dev/wiki/CodeReviewComments

Effective Go: https://go.dev/doc/effective_go#errors

## Examples

```go
value, err := load()
if err != nil {
    return fmt.Errorf("load: %w", err)
}
```
