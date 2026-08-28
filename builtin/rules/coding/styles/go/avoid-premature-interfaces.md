# Avoid premature Go interfaces

## Metadata

| Field | Value |
|---|---|
| ID | coding.styles.go.avoid-premature-interfaces |
| Description | Creates interfaces only when a real behavioral abstraction exists. |
| Scope | coding/go |
| Level | should-not |
| Tags | coding; go; style; interfaces; abstraction |

## Rule

Code should not introduce an interface solely because a type is named service, repository, manager, or similar, nor solely to enable mocking. Start with concrete behavior and introduce an interface when multiple implementations or a consumer boundary creates a real need.

## Exceptions

Framework or generated APIs may define required interfaces.

## Rationale

Go interfaces are satisfied implicitly, so unnecessary interface declarations add abstraction without adding capability.

## Sources

Go Style Best Practices: https://google.github.io/styleguide/go/best-practices

## Examples

Prefer a concrete `Store` implementation until a consumer actually needs a smaller behavioral contract.
