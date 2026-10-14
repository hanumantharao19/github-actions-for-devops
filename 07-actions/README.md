# 07 - Actions

GitHub Actions provides reusable actions that can be used inside workflow steps.

Until now, we primarily used:

```yaml
run:
  echo "Hello"
```

Now we will learn how to use:

```yaml
uses:
```

---

## `run` vs `uses`

### `run`

Executes a shell command.

```yaml
- name: Show Git version
  run: git --version
```

### `uses`

Uses an existing GitHub Action.

```yaml
- name: Checkout repository
  uses: actions/checkout@v4
```

---

# Learning Flow

```text
01 uses: Action
       |
       v
02 Checkout
       |
       v
03 Setup Node
       |
       v
04 Setup Python
       |
       v
05 Community Actions
```

---

# 1. Using an Action

The basic syntax is:

```yaml
- name: Action name
  uses: owner/repository@version
```

Example:

```yaml
- name: Checkout repository
  uses: actions/checkout@v4
```

---

# 2. Checkout Action

GitHub-hosted runners are temporary machines.

Your repository source code is not automatically available in the runner workspace.

The checkout action downloads the repository code into the runner.

```yaml
- name: Checkout repository
  uses: actions/checkout@v4
```

Typical CI flow:

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
Source Code
       |
       v
Build / Test
```

---

# 3. Setup Node

Node.js applications can use:

```yaml
uses: actions/setup-node@v4
```

This allows the workflow to install and configure a specific Node.js version.

Typical flow:

```text
Checkout
   |
   v
Setup Node
   |
   v
npm install
   |
   v
npm test
   |
   v
npm build
```

---

# 4. Setup Python

Python applications can use:

```yaml
uses: actions/setup-python@v5
```

Typical flow:

```text
Checkout
   |
   v
Setup Python
   |
   v
Install Dependencies
   |
   v
Run Tests
```

---

# 5. Community Actions

GitHub Marketplace and the GitHub Actions ecosystem provide many reusable actions.

Examples include actions for:

* Docker
* AWS
* Azure
* GCP
* Terraform
* Security scanning
* Code quality
* Notifications
* Deployment

Example structure:

```yaml
- name: Use an action
  uses: owner/action@version
```

---

# `uses:` Structure

```text
owner / repository @ version
   |          |          |
   |          |          +-- Version/tag
   |          +------------- Action repository
   +------------------------ Owner
```

Example:

```yaml
uses: actions/checkout@v4
```

means:

```text
Owner      = actions
Repository = checkout
Version    = v4
```

---

# Real-Time CI/CD Pipeline

A real CI pipeline may look like:

```text
Developer Push
      |
      v
GitHub Actions
      |
      v
Checkout
      |
      v
Setup Runtime
      |
      v
Install Dependencies
      |
      v
Build
      |
      v
Test
      |
      v
Security Scan
      |
      v
Docker Build
      |
      v
Deploy
```

Actions allow us to reuse common functionality instead of implementing everything ourselves.

---

# Important Concepts

After completing this section, you should understand:

* `uses`
* GitHub Actions
* Action repository
* Action version
* Checkout action
* Setup Node action
* Setup Python action
* Community actions
* `run` vs `uses`
* How actions fit into CI/CD
