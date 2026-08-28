# New Go packages include usage examples

## Metadata

| Field | Value |
|---|---|
| ID | coding.styles.go.new-packages-have-examples |
| Description | Provides runnable or testable examples for newly introduced public packages. |
| Scope | coding/go |
| Level | should |
| Tags | coding; go; style; documentation; examples |

## Rule

A new public package should include at least one concise example or test that demonstrates its intended usage and normal call sequence.

## Exceptions

A trivial internal package with no reusable API may omit a standalone example.

## Rationale

Examples communicate API intent and are integrated with Go documentation and testing conventions.

## Sources

Go Code Review Comments: https://go.dev/wiki/CodeReviewComments

## Examples

Use `ExampleFoo` functions or a focused test showing a complete public call sequence.
