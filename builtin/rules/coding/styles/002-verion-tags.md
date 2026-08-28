# Version comes from a published version identifier

## Metadata

| Field       | Value                                                                                          |
| ----------- | ---------------------------------------------------------------------------------------------- |
| ID          | general.version-from-published-identifier                                                      |
| Description | Official artifact versions are established by the version identifier published by the project. |
| Origin      | builtin                                                                                        |
| Language    | en                                                                                             |
| Scope       | project                                                                                        |
| Level       | must                                                                                           |
| Tags        | versioning; artifacts; releases; traceability                                                  |

## Rule

The official version of a generated artifact must be derived from the version identifier published by the project.

When the project uses Git, the published version identifier should normally be a published Git tag.

Projects using another version control system or release mechanism may use its equivalent published version identifier.

A local or unpublished version identifier may be used to prepare or test a release, but it does not establish an official artifact version.

If no published version identifier identifies the build, the artifact version must be `dev`.

## Exceptions

None.

## Rationale

Using the project's published version identifier as the source of truth keeps source, version history and distributed artifacts traceable to the same project state.

It also avoids maintaining artifact versions manually in multiple locations without coupling it to a specific version control system.

## Sources

IASI

## Examples

Git project with a published tag:

```text
git tag v0.1.0
git push origin v0.1.0

artifact version → v0.1.0
```

Build without a published version identifier:

```text
artifact version → dev
```

A project using a version control or release system other than Git may use its equivalent published version identifier.
