# Generated binaries are not versioned

## Metadata

| Field       | Value                                                            |
| ----------- | ---------------------------------------------------------------- |
| ID          | general.generated-binaries-not-versioned                         |
| Description | Generated binaries must not be stored as versioned source files. |
| Origin      | builtin                                                          |
| Language    | en                                                               |
| Scope       | project                                                          |
| Level       | must-not                                                         |
| Tags        | git; binaries; artifacts; repository                             |

## Rule

Generated binaries and executable artifacts must not be committed to the source code repository.

Build outputs may exist locally in directories such as `bin/`, but they must be excluded from version control.

Official binaries must be distributed as generated artifacts associated with a published version or release.

## Exceptions

None, unless the repository exists specifically to distribute binary artifacts.

## Rationale

Generated binaries can be reproduced from their source and build configuration.

Keeping them outside version control avoids unnecessary repository growth, binary diffs and ambiguity between source code and generated artifacts.

## Sources

IASI

## Examples

Preferred:

```text
repository/
├── cmd/
├── internal/
├── bin/          # ignored by Git
└── .gitignore
```

Not preferred:

```text
repository/
├── cmd/
├── internal/
└── bin/
    └── application.exe   # committed to Git
```
