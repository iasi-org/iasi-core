# Use any in modern Go

## Metadata

| Field | Value |
|---|---|
| ID | coding.styles.go.any-over-empty-interface |
| Description | Uses any instead of interface{} for unconstrained values in new Go code. |
| Scope | coding/go |
| Level | should |
| Tags | coding; go; style; types; generics |

## Rule

New Go code should use `any` rather than `interface{}` when expressing an unconstrained value type.

## Exceptions

Existing APIs may retain `interface{}` for compatibility or consistency.

## Rationale

`any` is the standard alias introduced for this purpose and is clearer in modern Go code.

## Sources

Go Style Decisions: https://google.github.io/styleguide/go/decisions

## Examples

Prefer `func Print(v any)` over `func Print(v interface{})` in new code.
