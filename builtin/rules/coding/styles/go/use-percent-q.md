# Use %q for ambiguous string output

## Metadata

| Field | Value |
|---|---|
| ID | coding.styles.go.use-percent-q |
| Description | Uses %q when displaying strings whose boundaries matter. |
| Scope | coding/go |
| Level | should |
| Tags | coding; go; style; formatting; diagnostics |

## Rule

Human-facing diagnostics should prefer `%q` when a string may be empty or contain whitespace or control characters and visible boundaries improve debugging.

## Exceptions

Normal prose output where quoting would reduce readability may use `%s`.

## Rationale

Quoted formatting makes empty and control-containing strings easier to diagnose.

## Sources

Go Style Decisions: https://google.github.io/styleguide/go/decisions

## Examples

Prefer `t.Fatalf("name = %q, want %q", got, want)` when string boundaries matter.
