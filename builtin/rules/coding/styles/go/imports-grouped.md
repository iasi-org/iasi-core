# Go import groups

## Metadata

| Field | Value |
|---|---|
| ID | coding.styles.go.imports-grouped |
| Description | Groups Go imports with standard library imports first. |
| Scope | coding/go |
| Level | must |
| Tags | coding; go; style; imports |

## Rule

Imports must be organized into groups separated by blank lines, with standard library packages in the first group. `goimports` should be used when available to maintain grouping automatically.

## Exceptions

Generated files may retain generator-produced import structure.

## Rationale

Consistent grouping separates standard-library dependencies from external and local dependencies.

## Sources

Go Code Review Comments: https://go.dev/wiki/CodeReviewComments

## Examples

```go
import (
    "fmt"
    "os"

    "example.com/project/pkg"
)
```
