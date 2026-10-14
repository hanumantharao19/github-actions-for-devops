# Shell Types

## Objective

Understand different shells that can be used to execute commands in GitHub Actions.

---

## What is a Shell?

A shell is a program that interprets and executes commands.

Examples:

```text
Bash
PowerShell
CMD
Python
```

---

## Default Shell

On Ubuntu runners, the default shell is generally Bash.

Example:

```yaml
runs-on: ubuntu-latest

steps:
  - run: echo "Hello"
```

---

## Specify a Shell

We can explicitly specify the shell.

```yaml
- name: Bash example
  shell: bash
  run: echo "Hello from Bash"
```

PowerShell:

```yaml
- name: PowerShell example
  shell: pwsh
  run: Write-Host "Hello from PowerShell"
```

Python:

```yaml
- name: Python example
  shell: python
  run: print("Hello from Python")
```

---

## Why is this important?

Different operating systems and projects may use different scripting languages.

For example:

```text
Linux
  |
  +-- Bash
  +-- Python

Windows
  |
  +-- PowerShell
  +-- CMD
```

---

## Important

The shell determines how the command is interpreted.
