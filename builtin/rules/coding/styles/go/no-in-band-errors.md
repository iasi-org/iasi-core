# No in-band Go errors

## Metadata

| Field | Value |
|---|---|
| ID | coding.styles.go.no-in-band-errors |
| Description | Uses separate error or ok results instead of sentinel data values for failure. |
| Scope | coding/go |
| Level | should |
| Tags | coding; go; style; errors; api |

## Rule

A function should not encode failure or absence through an otherwise valid data value such as `-1`, `""`, or `nil` when callers need to distinguish that state. Return an additional `error` or `ok` result instead.

## Exceptions

Established APIs where the sentinel is itself the intended semantic result may retain that contract.

## Rationale

Separate status results make failure explicit and prevent accidental use of invalid data.

## Sources

Go Code Review Comments: https://go.dev/wiki/CodeReviewComments

## Examples

```go
func Lookup(key string) (Value, bool)
```
