# Restrict blank imports

## Metadata

| Field | Value |
|---|---|
| ID | coding.styles.go.blank-imports-restricted |
| Description | Restricts side-effect-only imports to entry points or tests that require them. |
| Scope | coding/go |
| Level | should |
| Tags | coding; go; style; imports |

## Rule

Blank imports used only for side effects should be limited to `package main`, explicit registration points, or tests that genuinely require the side effect.

## Exceptions

Framework registration mechanisms may require documented blank imports.

## Rationale

Side-effect imports create hidden behavior and should appear only where their purpose is intentional and visible.

## Sources

Go Code Review Comments: https://go.dev/wiki/CodeReviewComments

## Examples

```go
import _ "net/http/pprof" // justified entry-point registration
```
