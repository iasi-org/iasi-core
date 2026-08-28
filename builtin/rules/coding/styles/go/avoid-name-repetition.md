# Avoid name repetition

## Metadata

| Field | Value |
|---|---|
| ID | coding.styles.go.avoid-name-repetition |
| Description | Avoids repeating package or type context in identifier names. |
| Scope | coding/go |
| Level | should |
| Tags | coding; go; style; naming; clarity |

## Rule

Names should omit information already made obvious by package, type, method, or local context. Exported names must be evaluated as they appear to package users.

## Exceptions

Additional context may be retained when omitting it would make the identifier ambiguous.

## Rationale

Go call sites naturally provide context through package and receiver names, so repetition adds noise.

## Sources

Effective Go: https://go.dev/doc/effective_go#package-names

Go Style Decisions: https://google.github.io/styleguide/go/decisions

## Examples

Prefer `bufio.Reader` over `bufio.BufReader`, and `project.Name()` over `project.ProjectName()` when the context is already clear.
