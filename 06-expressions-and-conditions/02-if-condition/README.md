# If Conditions

The `if` condition controls whether a job or step should execute.

Basic syntax:

```yaml
if: condition
```

---

## Example

```yaml
if: github.ref_name == 'main'
```

The step runs only when the branch is `main`.

---

## Step-Level Condition

```yaml
steps:

  - name: Deploy
    if: github.ref_name == 'main'
    run: echo "Deploying application"
```

---

## Job-Level Condition

Conditions can also be applied to jobs.

```yaml
jobs:

  deploy:
    if: github.ref_name == 'main'
    runs-on: ubuntu-latest

    steps:
      - name: Deploy
        run: echo "Deploying application"
```

---

## Real-Time Example

A common CI/CD pattern is:

```text
Feature Branch
     |
     v
    Build
     |
     v
    Test
     |
     v
Is main?
   /   \
 No     Yes
 |       |
Stop   Deploy
```

---

## Multiple Conditions

You can combine conditions.

```yaml
if: github.ref_name == 'main' && github.event_name == 'push'
```

This means:

```text
Branch = main
AND
Event = push
```

---

## Common Operators

```text
==     Equal
!=     Not equal
&&     AND
||     OR
!      NOT
```

Conditions are very important for deployment pipelines.
