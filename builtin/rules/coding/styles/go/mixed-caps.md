# Go identifier casing

## Metadata

| Field | Value |
|---|---|
| ID | coding.styles.go.mixed-caps |
| Description | Uses MixedCaps instead of underscores for multiword Go identifiers. |
| Scope | coding/go |
| Level | must |
| Tags | coding; go; style; naming |

## Rule

Multiword Go identifiers must use `MixedCaps` or `mixedCaps`, not snake_case or underscore-separated names.

## Exceptions

Generated identifiers or identifiers required by an external protocol may retain the externally defined spelling.

## Rationale

MixedCaps is the established naming convention for Go source code.

## Sources

Effective Go: https://go.dev/doc/effective_go#mixed-caps

Go Style Guide: https://google.github.io/styleguide/go/guide#mixed-caps

## Examples

Preferred:

```go
maxRetries := 3
type HTTPClient struct{}
```

Avoid:

```go
max_retries := 3
```
