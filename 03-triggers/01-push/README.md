# Push Trigger

## Objective

Learn how to configure a workflow that runs when code is pushed to specific branches.

---

## Basic Push Trigger

A workflow can be triggered by a push:

```yaml
on:
  push:
```

This runs for pushes to different branches.

---

## Branch Filtering

We can restrict the workflow to specific branches.

```yaml
on:
  push:
    branches:
      - main
      - develop
```

Now the workflow runs only when code is pushed to:

```text
main
develop
```

---

## Ignore Branches

We can also exclude branches:

```yaml
on:
  push:
    branches-ignore:
      - feature/*
```

This prevents the workflow from running for matching feature branches.

---

## Real-Time Example

We may want production-related workflows to run only when code is pushed to `main`.

```text
feature branch
      |
      v
     push
      |
      X
   No deployment

main
 |
 push
 |
 v
Run workflow
```

---

## Important

`push` is the event.

`branches` and `branches-ignore` are filters.

Example:

```yaml
on:
  push:
    branches:
      - main
```

This means:

> Run the workflow when code is pushed to `main`.
