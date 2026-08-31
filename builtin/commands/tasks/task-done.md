# Complete task

## Metadata

| Field | Value |
|---|---|
| ID | task.done |
| Description | Completes one or more active tasks using their existing execution result. |
| Origin | builtin |
| Language | en |
| Applies | |

## Usage

```text
task.done(
    selector
)
```

## Parameters

| Name | Required | Default | Description |
|---|---|---|---|
| selector | yes | | Primary parameter. Selects zero, one, or multiple active tasks. |

The primary parameter may be provided positionally:

```text
task.done("001-create-binary")
```

or by name:

```text
task.done(
    selector = "001-create-binary"
)
```

Quoted values are literals. Unquoted values are references resolved from the current execution context.

## Purpose

Explicitly complete active tasks whose execution result already exists.

`task.done` does not choose or create the outcome.

The outcome is a result of execution and is only consolidated by this command.

## Selector

A selector identifies zero, one, or multiple tasks.

The canonical model does not prescribe a specific selector syntax.

Adapters may support identifiers, patterns, sets, expressions, queries, filters, or other suitable mechanisms.

If the selector matches no applicable tasks, the command must produce a warning and complete without changing state.

If the selector matches multiple tasks, the complete target set must be resolved before applying changes.


Only tasks in the `active` state with an execution result suitable for completion are applicable to this command.

## Preconditions

For every applicable selected task:

- the task must exist;
- the task must be `active`;
- an execution result must exist;
- the task must be ready for explicit completion.

## Operation

Complete every applicable selected task using its existing execution outcome.

Conceptually:

```text
run
 ↓
execution result
 ↓
outcome
 ↓
task.done
 ↓
done/<outcome>
```

## Effects

Each selected task moves from `active` to the corresponding `done/<outcome>` state.

Possible outcomes may include:

```text
success
failed
partial
cancelled
```

The task definition must not be modified solely because of completion.

Completing a task does not imply that its result has been validated.

```text
done != validated
```

## Outputs

For each affected task:

- task reference;
- previous state: `active`;
- current state: `done`;
- existing outcome.

The output may be used as the primary input of a compatible chained command.

## Warnings

If no applicable tasks match the selector, produce a warning and perform no changes.

## Errors

The command must fail when:

- the task has no execution result to consolidate;
- an unquoted reference cannot be resolved;
- completion cannot be performed safely.

## Examples

```text
task.done("001-create-binary")
```

```text
task.done(
    selector = current_task
)
```
