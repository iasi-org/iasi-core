# Accept interfaces, return concrete types

## Metadata

| Field | Value |
|---|---|
| ID | coding.styles.go.accept-interfaces-return-concrete |
| Description | Prefers interface parameters and concrete return values when designing APIs. |
| Scope | coding/go |
| Level | should |
| Tags | coding; go; style; interfaces; api |

## Rule

Functions should prefer accepting the minimal interface behavior they need and returning concrete implementation types when doing so preserves useful capability for callers.

## Exceptions

Returning an interface is appropriate when encapsulation, protocol semantics, factories, or an established API require it.

## Rationale

This pattern reduces caller constraints while avoiding premature loss of concrete capabilities.

## Sources

Go Style Decisions: https://google.github.io/styleguide/go/decisions

## Examples

Prefer `func Parse(r io.Reader) (*Document, error)` over requiring a concrete reader type or returning an unnecessary `Document` interface.
