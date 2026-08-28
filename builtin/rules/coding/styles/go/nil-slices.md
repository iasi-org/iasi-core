# Prefer nil slices when empty

## Metadata

| Field | Value |
|---|---|
| ID | coding.styles.go.nil-slices |
| Description | Uses nil slices as the normal empty slice representation. |
| Scope | coding/go |
| Level | should |
| Tags | coding; go; style; slices; zero-values |

## Rule

When an empty slice has no required serialization distinction, prefer the nil zero value (`var items []T`) over allocating an empty non-nil slice (`items := []T{}`).

## Exceptions

Use an empty non-nil slice when an external encoding or API contract distinguishes `[]` from `null`, or when the distinction is otherwise semantically required.

## Rationale

Nil slices behave like empty slices for common operations while preserving useful zero-value semantics.

## Sources

Go Code Review Comments: https://go.dev/wiki/CodeReviewComments

## Examples

Prefer `var items []string` unless an API specifically requires a non-nil empty slice.
