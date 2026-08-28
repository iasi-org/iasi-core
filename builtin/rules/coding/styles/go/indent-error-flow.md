# Go error flow first

## Metadata

| Field | Value |
|---|---|
| ID | coding.styles.go.indent-error-flow |
| Description | Handles errors and terminal branches before the normal path. |
| Scope | coding/go |
| Level | must |
| Tags | coding; go; style; errors; control-flow |

## Rule

Error and terminal conditions should be handled first and return or continue immediately. The normal path should remain unindented and should not be placed in an unnecessary `else` branch after a terminal condition.

## Exceptions

None.

## Rationale

Keeping the successful path at the lowest indentation level improves line of sight and reduces nesting.

## Sources

Go Code Review Comments: https://go.dev/wiki/CodeReviewComments

Go Style Decisions: https://google.github.io/styleguide/go/decisions

## Examples

Preferred:

```go
if err != nil {
    return err
}
process()
```
