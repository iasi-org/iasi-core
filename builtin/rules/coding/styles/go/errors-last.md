# Go errors returned last

## Metadata

| Field | Value |
|---|---|
| ID | coding.styles.go.errors-last |
| Description | Returns error as the final result when a function can fail. |
| Scope | coding/go |
| Level | must |
| Tags | coding; go; style; errors; api |

## Rule

When a function returns an `error`, the `error` result must be the final return value. Exported functions must expose failures using the `error` interface rather than a concrete error pointer type.

## Exceptions

Signatures imposed by an external interface may be followed as defined.

## Rationale

Returning `error` last is a core Go API convention and makes call sites predictable.

## Sources

Go Style Decisions: https://google.github.io/styleguide/go/decisions

## Examples

```go
func Load(path string) (*Config, error) { ... }
```
