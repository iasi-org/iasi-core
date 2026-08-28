# Go receiver names

## Metadata

| Field | Value |
|---|---|
| ID | coding.styles.go.receiver-names |
| Description | Uses short, type-related, consistent receiver names. |
| Scope | coding/go |
| Level | must |
| Tags | coding; go; style; naming; receivers |

## Rule

Method receiver names must be short, normally one or two letters, derived from the receiver type, and used consistently for that type. Generic object-oriented names such as `this`, `self`, or `me` must not be used.

## Exceptions

None.

## Rationale

A receiver is an ordinary Go parameter whose role is already obvious from the method declaration.

## Sources

Go Code Review Comments: https://go.dev/wiki/CodeReviewComments

Go Style Decisions: https://google.github.io/styleguide/go/decisions

## Examples

Preferred:

```go
func (c *Client) Close() error { ... }
```

Avoid:

```go
func (this *Client) Close() error { ... }
```
