# Consumer-defined Go interfaces

## Metadata

| Field | Value |
|---|---|
| ID | coding.styles.go.interfaces-consumer-defined |
| Description | Defines interfaces near the code that consumes them. |
| Scope | coding/go |
| Level | should |
| Tags | coding; go; style; interfaces; architecture |

## Rule

An interface should normally be defined by the package that consumes the behavior, containing only the methods that consumer actually needs.

## Exceptions

A package may export an interface when the interface itself is the product or a shared protocol contract.

## Rationale

Consumer-defined interfaces avoid speculative abstractions and unnecessary coupling to producer implementations.

## Sources

Go Style Decisions: https://google.github.io/styleguide/go/decisions

Go Style Best Practices: https://google.github.io/styleguide/go/best-practices

## Examples

A package needing only `Read([]byte)` should depend on that behavior rather than a large producer-defined service interface.
