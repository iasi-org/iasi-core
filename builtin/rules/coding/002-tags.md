# Version comes from a published version tag

## Metadata

| Field       | Value                                                             |
| ----------- | ----------------------------------------------------------------- |
| ID          | general.version-from-published-tag                                |
| Description | Official artifact versions are established by the version identifier published by the project. |
| Origin      | builtin                                                           |
| Language    | en                                                                |
| Scope       | project                                                           |
| Level       | must                                                              |
| Tags        | git; versioning; tags; artifacts                                  |

## Rule

The official version of a generated artifact must be derived from the version tag that identifies the published version.

A local tag may be used to prepare or test a release, but it does not establish an official version until it has been published to the project's remote repository.

Builds not associated with a published version tag must be identified as development builds.

## Exceptions

None.

## Rationale

Using published Git tags as the source of truth keeps source code, version history and distributed artifacts traceable to the same immutable repository state.

It also avoids maintaining version numbers manually in multiple locations.

## Sources

IASI

## Examples

Published version:

```text
git tag v0.1.0
git push origin v0.1.0

artifact version → v0.1.0
```

Development build:

```text
no published version tag

artifact version → dev
```
