# No panic for normal errors

## Metadata

| Field | Value |
|---|---|
| ID | coding.styles.go.no-panic-normal-errors |
| Description | Avoids panic for ordinary error handling. |
| Scope | coding/go |
| Level | must-not |
| Tags | coding; go; style; errors; panic |

## Rule

`panic` must not be used for errors that callers can reasonably encounter and handle. Such failures must be represented through normal Go error handling.

## Exceptions

A panic may be appropriate for truly impossible internal invariants or programmer errors where continuing would be invalid.

## Rationale

Panic bypasses ordinary error control flow and is not the idiomatic mechanism for expected failure.

## Sources

Go Code Review Comments: https://go.dev/wiki/CodeReviewComments

Effective Go: https://go.dev/doc/effective_go#panic

## Examples

Prefer returning `error` for invalid input, missing files, network failures, or rejected configuration.
