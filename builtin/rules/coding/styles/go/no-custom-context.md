# No custom Go context types

## Metadata

| Field | Value |
|---|---|
| ID | coding.styles.go.no-custom-context |
| Description | Uses context.Context directly rather than custom context abstractions. |
| Scope | coding/go |
| Level | must-not |
| Tags | coding; go; style; context; api |

## Rule

Code must not define custom context types or replace `context.Context` with project-specific context interfaces in function signatures.

## Exceptions

None.

## Rationale

Custom context abstractions break interoperability and make propagation across packages unnecessarily complex.

## Sources

Go Code Review Comments: https://go.dev/wiki/CodeReviewComments

Go Style Decisions: https://google.github.io/styleguide/go/decisions

## Examples

Use `context.Context` directly.
