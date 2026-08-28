# Go getter names

## Metadata

| Field | Value |
|---|---|
| ID | coding.styles.go.getter-names |
| Description | Avoids Get prefixes for simple Go getters. |
| Scope | coding/go |
| Level | should-not |
| Tags | coding; go; style; naming; methods |

## Rule

A simple getter method should normally be named after the property it returns rather than using a `Get` prefix. Setter methods may use `Set` when appropriate.

## Exceptions

External interfaces or generated APIs may require getter names with a `Get` prefix.

## Rationale

Go method calls already communicate invocation, so a `Get` prefix usually adds no useful information.

## Sources

Effective Go: https://go.dev/doc/effective_go#Getters

## Examples

Prefer `obj.Owner()` and `obj.SetOwner(user)` over `obj.GetOwner()`.
