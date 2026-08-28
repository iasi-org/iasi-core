# Go variable name scope

## Metadata

| Field | Value |
|---|---|
| ID | coding.styles.go.variable-name-scope |
| Description | Makes variable names more descriptive as their scope increases. |
| Scope | coding/go |
| Level | should |
| Tags | coding; go; style; naming; variables |

## Rule

Local variable names may be short when their scope and meaning are obvious. Names must become more descriptive as the distance between declaration and use increases.

## Exceptions

Conventional names such as `i`, `r`, `w`, `ctx`, or `err` may remain short when their meaning is idiomatic and clear.

## Rationale

Name length should reflect the amount of context the reader needs, not a blanket verbosity rule.

## Sources

Go Code Review Comments: https://go.dev/wiki/CodeReviewComments

## Examples

`i` is appropriate for a short loop index. A package-level value should normally use a more descriptive name.
