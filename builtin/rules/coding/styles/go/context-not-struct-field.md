# Do not store context in structs

## Metadata

| Field | Value |
|---|---|
| ID | coding.styles.go.context-not-struct-field |
| Description | Passes context explicitly instead of storing it as object state. |
| Scope | coding/go |
| Level | must-not |
| Tags | coding; go; style; context; structs |

## Rule

A `context.Context` should not be stored as a struct field. Methods that need a context should accept it explicitly as a parameter.

## Exceptions

An external interface or framework contract may impose a context-bearing structure.

## Rationale

Contexts have request-scoped lifetimes and should flow explicitly with the operations they control.

## Sources

Go Code Review Comments: https://go.dev/wiki/CodeReviewComments

Go Style Decisions: https://google.github.io/styleguide/go/decisions

## Examples

Prefer `func (s *Service) Load(ctx context.Context)` over storing `ctx` in `Service`.
