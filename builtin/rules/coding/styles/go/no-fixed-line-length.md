# Go line length

## Metadata

| Field | Value |
|---|---|
| ID | coding.styles.go.no-fixed-line-length |
| Description | Does not impose a fixed maximum line length on Go source. |
| Scope | coding/go |
| Level | must |
| Tags | coding; go; style; formatting; line-length |

## Rule

Go source must not be reformatted solely to satisfy a fixed character-column limit. Long lines should be restructured when readability benefits, using `gofmt` as the formatting authority.

## Exceptions

Project-specific requirements may impose a limit for generated displays or external tooling.

## Rationale

Go intentionally has no canonical fixed line length; readability and canonical formatting take precedence.

## Sources

Go Code Review Comments: https://go.dev/wiki/CodeReviewComments

Go Style Decisions: https://google.github.io/styleguide/go/decisions

## Examples

A readable 110-character expression may remain intact if splitting it makes the code harder to understand.
