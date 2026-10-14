# Checkout Action

The checkout action downloads the repository source code into the GitHub Actions runner.

The commonly used action is:

```yaml
uses: actions/checkout@v4
```

---

## Why Do We Need Checkout?

A GitHub-hosted runner is a temporary machine.

Your repository source code needs to be checked out into the runner workspace before many build or test commands can use it.

The flow is:

```text
GitHub Repository
       |
       v
GitHub Actions Runner
       |
       v
actions/checkout
       |
       v
Repository Files
```

---

## Example

```yaml
steps:

  - name: Checkout repository
    uses: actions/checkout@v4

  - name: List files
    run: ls -la
```

---

## Real-Time CI/CD

Almost every application CI pipeline starts with something similar to:

```text
Checkout
   |
   v
Build
   |
   v
Test
   |
   v
Package
   |
   v
Deploy
```

For example:

```yaml
- name: Checkout repository
  uses: actions/checkout@v4

- name: Install dependencies
  run: npm install

- name: Run tests
  run: npm test
```

---

## Important

The checkout action does not build or test your application.

Its main responsibility is to make the repository source code available to the runner.
