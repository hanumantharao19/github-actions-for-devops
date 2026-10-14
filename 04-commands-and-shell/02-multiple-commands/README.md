# Multiple Commands

## Objective

Learn how to execute multiple shell commands inside one GitHub Actions step.

---

## Multiple Commands

We can use the `|` symbol to execute multiple commands.

```yaml
run: |
  pwd
  ls -la
  echo "Hello"
```

Each command executes sequentially.

---

## Example

```text
Step
 |
 +-- pwd
 |
 +-- ls
 |
 +-- whoami
 |
 +-- date
```

---

## Why Use Multiple Commands?

Sometimes several related commands belong to the same task.

Example:

```yaml
- name: Build application
  run: |
    npm install
    npm test
    npm run build
```

---

## Important

Commands normally execute in the order in which they are written.

If an earlier command fails, later commands may not execute normally.
