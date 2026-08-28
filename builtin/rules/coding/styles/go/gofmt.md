# Go formatting

## Metadata

| Field | Value |
|---|---|
| ID | coding.styles.go.gofmt |
| Description | All Go source must be formatted with gofmt. |
| Scope | coding/go |
| Level | must |
| Tags | coding; go; style; formatting |

## Rule

All Go source files must conform to the formatting produced by `gofmt`. Formatting must not be maintained manually in a style that conflicts with `gofmt`.

## Exceptions

Generated or externally vendored source may retain its upstream formatting when it is not owned by the project.

## Rationale

`gofmt` is the canonical formatting convention of the Go ecosystem and removes unnecessary style debate.

## Sources

Effective Go: https://go.dev/doc/effective_go

Go Style Guide: https://google.github.io/styleguide/go/guide

## Examples

Preferred:

```bash
gofmt -w .
```
