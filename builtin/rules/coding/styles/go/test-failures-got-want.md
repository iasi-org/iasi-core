# Go test failures use got/want

## Metadata

| Field | Value |
|---|---|
| ID | coding.styles.go.test-failures-got-want |
| Description | Writes diagnostic test failures with actual value before expected value. |
| Scope | coding/go |
| Level | should |
| Tags | coding; go; testing; diagnostics |

## Rule

Test failure messages should identify the operation or input when useful and report the actual value before the expected value, using `got` and `want` terminology.

## Exceptions

Specialized diff output may use another order when the direction is explicitly labeled.

## Rationale

Consistent, information-rich failures reduce the time required to diagnose tests.

## Sources

Go Code Review Comments: https://go.dev/wiki/CodeReviewComments

Go Style Decisions: https://google.github.io/styleguide/go/decisions

## Examples

```go
if got != want {
    t.Errorf("Parse(%q) = %v, want %v", input, got, want)
}
```
