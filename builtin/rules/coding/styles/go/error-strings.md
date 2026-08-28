# Go error strings

## Metadata

| Field | Value |
|---|---|
| ID | coding.styles.go.error-strings |
| Description | Uses composable Go error message style. |
| Scope | coding/go |
| Level | must |
| Tags | coding; go; style; errors; messages |

## Rule

Error strings should start with lowercase text unless beginning with a proper noun or acronym, and should not end with punctuation.

## Exceptions

User-facing log or UI messages may use normal sentence capitalization and punctuation.

## Rationale

Errors are frequently wrapped inside larger messages, so sentence-style capitalization and punctuation compose poorly.

## Sources

Go Code Review Comments: https://go.dev/wiki/CodeReviewComments

Go Style Decisions: https://google.github.io/styleguide/go/decisions

## Examples

Preferred: `fmt.Errorf("open config: %w", err)`

Avoid: `fmt.Errorf("Open config failed.")`
