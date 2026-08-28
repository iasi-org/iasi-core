# Go type aliases are exceptional

## Metadata

| Field | Value |
|---|---|
| ID | coding.styles.go.type-aliases-rare |
| Description | Uses type aliases primarily for migration rather than routine type design. |
| Scope | coding/go |
| Level | should-not |
| Tags | coding; go; style; types; aliases |

## Rule

Type aliases (`type A = B`) should not be used when a new defined type (`type A B`) or direct use of the original type expresses the intent. Aliases are primarily appropriate for package migration and compatibility.

## Exceptions

Migration, compatibility, or generated code may require aliases.

## Rationale

Aliases do not create a distinct type and can hide architectural boundaries when used casually.

## Sources

Go Style Decisions: https://google.github.io/styleguide/go/decisions

## Examples

Use `type UserID string` when a distinct domain type is intended; reserve `type OldName = NewName` for compatibility/migration.
