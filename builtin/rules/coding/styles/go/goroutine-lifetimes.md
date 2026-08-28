# Go goroutine lifetimes

## Metadata

| Field | Value |
|---|---|
| ID | coding.styles.go.goroutine-lifetimes |
| Description | Makes goroutine termination conditions explicit. |
| Scope | coding/go |
| Level | must |
| Tags | coding; go; style; concurrency; goroutines |

## Rule

Every spawned goroutine must have a clear and reviewable termination condition. When the lifetime is not obvious from the code, it must be documented and tied to cancellation, channel closure, completion, or another explicit mechanism.

## Exceptions

Long-lived process goroutines may intentionally live for the process lifetime when that is part of the program design.

## Rationale

Unbounded goroutine lifetimes cause leaks, races, and unpredictable resource use.

## Sources

Go Code Review Comments: https://go.dev/wiki/CodeReviewComments

## Examples

A worker goroutine should normally exit on `ctx.Done()`, input-channel closure, or completion of its assigned work.
