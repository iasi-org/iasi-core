# Execute task

## Metadata

| Field | Value |
|---|---|
| ID | task.execute |
| Description | Executes one or more active tasks. |
| Origin | builtin |
| Language | en |
| Applies | |

## Purpose

Execute the work defined by tasks that are currently active.

A task may be executed more than once while it remains active.

## Inputs

- Task selector.
- Completion mode: `auto` or `manual`.

## Selector

A selector identifies zero, one, or multiple tasks.

The selector mechanism is canonical and does not prescribe a specific syntax such as globbing.

A selector may be implemented by adapters using identifiers, patterns, sets, expressions, or other suitable mechanisms.

If the selector matches no applicable tasks, the command must produce a warning and complete without changing state.

If the selector matches multiple tasks, the complete target set must be resolved before applying changes.


Only tasks in the `active` state are applicable to this command.

## Completion mode

### auto

When execution completes successfully and the task is considered complete, the task may transition automatically from `active` to `done`.

If execution fails or remains incomplete, the task remains `active`.

### manual

The task remains `active` after successful execution.

A separate explicit `task.done` operation is required to mark the task as completed.

This mode is intended for tasks that require manual review, inspection, approval, or another explicit decision before completion.

## Preconditions

For every applicable selected task:

- the task must exist;
- the task must be in the `active` state;
- the executor must have access to the context required by the task.

## Operation

Execute the work described by every applicable selected task using the applicable project context.

Execution may be repeated as many times as required while the task remains active.

## Effects

Execution may modify project artifacts as required by the task.

With `completion=manual`, task state remains `active`.

With `completion=auto`, a successfully completed task may transition to `done`.

## Outputs

For each affected task:

- task identifier;
- execution result;
- resulting task state.

## Errors

The command must report execution failures for affected tasks.

A failed or incomplete execution must not mark the task as `done`.

No matches are not an error and must produce a warning.

## Examples

Automatic completion:

```text
task.execute(selector, completion=auto)
```

Manual completion:

```text
task.execute(selector, completion=manual)
```

Repeated execution:

```text
active
  -> execute
  -> active
  -> execute
  -> active
  -> execute
  -> done
```
