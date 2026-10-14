# Working Directory

## Objective

Learn how to execute commands from a specific directory.

---

## Default Working Directory

GitHub Actions normally executes commands from the workspace directory.

Example:

```yaml
- name: Show directory
  run: pwd
```

---

## `working-directory`

We can specify another directory.

```yaml
- name: Run from application directory
  working-directory: ./application
  run: pwd
```

The command executes from:

```text
application/
```

---

## Real-Time Example

Consider:

```text
project/
├── application/
├── terraform/
└── scripts/
```

We can run:

```yaml
- name: Run application commands
  working-directory: ./application
  run: |
    ls
    echo "Building application"
```

And:

```yaml
- name: Run Terraform
  working-directory: ./terraform
  run: terraform init
```

---

## Important

`working-directory` is useful when a repository contains multiple projects or components.
