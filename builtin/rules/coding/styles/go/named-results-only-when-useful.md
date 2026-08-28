# Go named results only when useful

## Metadata

| Field | Value |
|---|---|
| ID | coding.styles.go.named-results-only-when-useful |
| Description | Uses named result parameters only when they clarify meaning. |
| Scope | coding/go |
| Level | should |
| Tags | coding; go; style; functions; returns |

## Rule

Result parameters should be named only when the names clarify otherwise ambiguous results or are required by deferred logic. They should not be named merely to save local declarations or enable naked returns.

## Exceptions

Multiple results of the same type may benefit from names, such as latitude and longitude.

## Rationale

Unnecessary result names make public signatures noisier without improving understanding.

## Sources

Go Code Review Comments: https://go.dev/wiki/CodeReviewComments

## Examples

Prefer `func Parent() (*Node, error)` over `func Parent() (node *Node, err error)` when the result meaning is already clear.
