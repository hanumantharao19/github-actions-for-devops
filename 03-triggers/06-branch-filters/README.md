# Branch Filters

## Objective

Learn how to run workflows only for specific Git branches.

---

## Why Branch Filters?

Real projects normally have multiple branches.

Example:

```text
main
develop
feature/*
release/*
```

Different actions may be required for different branches.

---

## Include Specific Branches

```yaml
on:
  push:
    branches:
      - main
      - develop
```

The workflow runs only for:

```text
main
develop
```

---

## Wildcards

We can use patterns.

```yaml
on:
  push:
    branches:
      - 'feature/**'
```

This matches feature branches.

---

## Ignore Branches

```yaml
on:
  push:
    branches-ignore:
      - 'feature/**'
```

This runs for all branches except matching feature branches.

---

## Real-Time Example

```text
feature/*
     |
     | Push
     v
    CI

develop
     |
     | Push
     v
   CI + Build

main
     |
     | Push
     v
 CI + Build + Deploy
```

Branch filters are commonly used to implement different CI/CD behavior for different branches.
