# No dot imports

## Metadata

| Field | Value |
|---|---|
| ID | coding.styles.go.no-dot-imports |
| Description | Disallows dot imports in normal Go code. |
| Scope | coding/go |
| Level | must-not |
| Tags | coding; go; style; imports |

## Rule

Go source must not use dot imports because they hide the package origin of referenced identifiers.

## Exceptions

A narrowly justified external test package may use a dot import when circular dependency constraints make it necessary.

## Rationale

Explicit package qualification improves readability and makes dependencies visible.

## Sources

Go Code Review Comments: https://go.dev/wiki/CodeReviewComments

## Examples

Avoid:

```go
import . "example.com/project/pkg"
```
