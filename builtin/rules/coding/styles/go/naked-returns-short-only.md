# Limit naked returns

## Metadata

| Field | Value |
|---|---|
| ID | coding.styles.go.naked-returns-short-only |
| Description | Restricts naked returns to very small, obvious functions. |
| Scope | coding/go |
| Level | should |
| Tags | coding; go; style; functions; returns |

## Rule

A naked `return` should be used only in a very short function where the named results remain immediately obvious. Medium or long functions must return values explicitly.

## Exceptions

Deferred closures that intentionally update named results may justify named results, but explicit returns are still preferred when clearer.

## Rationale

Explicit return values reduce the cognitive load of tracking mutable named results through a function.

## Sources

Go Code Review Comments: https://go.dev/wiki/CodeReviewComments

## Examples

In a multi-step function, prefer `return result, err` over a bare `return`.
