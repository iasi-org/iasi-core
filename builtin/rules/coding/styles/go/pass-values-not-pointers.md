# Pass Go values when pointers add no semantics

## Metadata

| Field | Value |
|---|---|
| ID | coding.styles.go.pass-values-not-pointers |
| Description | Avoids pointers used only to save small copies. |
| Scope | coding/go |
| Level | should |
| Tags | coding; go; style; pointers; api |

## Rule

Values should be passed directly when pointer semantics are not required. In particular, pointers to strings and pointers to interface values should not be used merely to avoid copying a small fixed-size value.

## Exceptions

Large structs, mutable shared state, optional semantics, or types expected to grow may justify pointers.

## Rationale

Pointers should communicate semantics, not be used as a reflexive micro-optimization.

## Sources

Go Code Review Comments: https://go.dev/wiki/CodeReviewComments

Go Style Decisions: https://google.github.io/styleguide/go/decisions

## Examples

Prefer `func Print(s string)` over `func Print(s *string)` when the function only reads the string.
