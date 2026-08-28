# Avoid generic Go package names

## Metadata

| Field | Value |
|---|---|
| ID | coding.styles.go.avoid-generic-package-names |
| Description | Avoids uninformative packages such as util, common, misc, or helpers. |
| Scope | coding/go |
| Level | should-not |
| Tags | coding; go; style; packages; naming |

## Rule

Packages should not use broad, uninformative names such as `util`, `common`, `misc`, `helper`, `helpers`, `model`, or `types` when a domain-specific name can express the package purpose.

## Exceptions

A genuinely narrow and established package may retain such a name when changing it would reduce clarity or break compatibility.

## Rationale

Specific package names communicate responsibility and reduce import renaming and ambiguity.

## Sources

Go Code Review Comments: https://go.dev/wiki/CodeReviewComments

Go Style Decisions: https://google.github.io/styleguide/go/decisions

## Examples

Prefer `archive`, `retry`, or `config` over `util` or `common` when those names describe the actual responsibility.
