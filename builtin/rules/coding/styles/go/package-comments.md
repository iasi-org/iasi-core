# Go package comments

## Metadata

| Field | Value |
|---|---|
| ID | coding.styles.go.package-comments |
| Description | Requires package documentation for public packages. |
| Scope | coding/go |
| Level | must |
| Tags | coding; go; style; documentation; packages |

## Rule

A public package must include a package comment adjacent to a `package` clause. The comment should explain the purpose of the package rather than merely restating its name.

## Exceptions

Small internal-only packages may omit a package comment when no exported API documentation is produced.

## Rationale

Package documentation is the entry point for users reading generated Go documentation.

## Sources

Go Code Review Comments: https://go.dev/wiki/CodeReviewComments

## Examples

```go
// Package config loads and validates application configuration.
package config
```
