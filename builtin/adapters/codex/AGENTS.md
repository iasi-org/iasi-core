# IASI

This project uses the IASI methodology.

## Project context

Before performing work, inspect the available context under `.iasi/`.

Use the applicable:

- inputs
- rules
- tasks

Do not invent requirements, decisions, or constraints that are not supported by the available context.

## Tasks

Tasks follow this lifecycle:

pending → active → done

Completed tasks may finish as:

- success
- failed
- partial
- cancelled

Use the canonical IASI task operations:

- `task.start`
- `task.run`
- `task.done`
- `task.rerun`
- `task.reopen`

Do not modify a task definition solely to change its state or outcome.

## Execution

When executing a task:

1. Read the task.
2. Read the applicable project context.
3. Respect all applicable rules.
4. Perform only work within the task scope.
5. Run the validations required by the task.
6. Report the execution result clearly.