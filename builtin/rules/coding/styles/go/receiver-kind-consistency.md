# Consistent Go receiver kind

## Metadata

| Field | Value |
|---|---|
| ID | coding.styles.go.receiver-kind-consistency |
| Description | Uses pointer or value receivers consistently for a type. |
| Scope | coding/go |
| Level | should |
| Tags | coding; go; style; receivers; pointers |

## Rule

Methods on the same type should normally use a consistent receiver kind. When in doubt for mutable or nontrivial structs, prefer pointer receivers.

## Exceptions

A type may legitimately mix receiver kinds when language semantics or interface implementation require it and the choice remains clear.

## Rationale

Consistent receiver semantics reduce accidental copying and make mutability expectations easier to understand.

## Sources

Go Style Decisions: https://google.github.io/styleguide/go/decisions

## Examples

Avoid arbitrarily mixing `func (t T)` and `func (t *T)` methods without a semantic reason.
