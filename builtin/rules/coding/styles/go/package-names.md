# Go package names

## Metadata

| Field | Value |
|---|---|
| ID | coding.styles.go.package-names |
| Description | Uses short, lowercase, single-word package names. |
| Scope | coding/go |
| Level | must |
| Tags | coding; go; style; packages; naming |

## Rule

Package names must be short, concise, lowercase, and normally a single word. They should not use underscores or mixed caps.

## Exceptions

A package whose established public identity requires a different form may retain it when compatibility outweighs renaming.

## Rationale

Package names qualify every exported identifier and should therefore be brief and readable at call sites.

## Sources

Effective Go: https://go.dev/doc/effective_go#package-names

Go Code Review Comments: https://go.dev/wiki/CodeReviewComments

## Examples

Preferred: `bytes`, `http`, `json`.

Avoid: `string_utils`, `HTTPHelpers`.
