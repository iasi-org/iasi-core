# Go doc comments

## Metadata

| Field | Value |
|---|---|
| ID | coding.styles.go.doc-comments |
| Description | Documents exported declarations with proper Go doc comments. |
| Scope | coding/go |
| Level | must |
| Tags | coding; go; style; documentation; comments |

## Rule

Exported packages, types, functions, methods, constants, and variables must have useful doc comments when they form part of the public API. A declaration doc comment should normally begin with the declared name and form a complete sentence.

## Exceptions

Obvious generated declarations may rely on generator documentation.

## Rationale

Go documentation tooling extracts declaration comments directly, making comment shape part of the public API experience.

## Sources

Effective Go: https://go.dev/doc/effective_go#commentary

Go Code Review Comments: https://go.dev/wiki/CodeReviewComments

## Examples

```go
// Encode writes the encoded representation of req.
func Encode(req Request) ([]byte, error) { ... }
```
