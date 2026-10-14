# Community Actions

GitHub Actions has a large ecosystem of reusable actions created by GitHub, vendors, open-source projects, and the community.

---

## Official Actions

Examples:

```text
actions/checkout
actions/setup-node
actions/setup-python
```

Example:

```yaml
uses: actions/checkout@v4
```

---

## Community and Vendor Actions

Actions are also available from other organizations.

Examples can provide functionality for:

```text
AWS
Azure
GCP
Docker
Terraform
Security scanning
Code quality
Notifications
Deployment
```

The general syntax remains:

```yaml
uses: owner/repository@version
```

---

## Example

A workflow might contain:

```yaml
steps:

  - name: Checkout
    uses: actions/checkout@v4

  - name: Setup Node.js
    uses: actions/setup-node@v4
    with:
      node-version: '20'
```

---

## How to Choose an Action

Before using a community action, check:

```text
1. Who maintains it?
2. Is the repository active?
3. How many users/stars does it have?
4. Is documentation available?
5. What permissions does it require?
6. What version should be used?
7. Is it trustworthy?
```

Security is especially important because an action executes code inside your workflow.

---

## Real-Time DevOps

In a production CI/CD pipeline, you may use actions for:

```text
Source Checkout
      |
      v
Runtime Setup
      |
      v
Code Quality
      |
      v
Security Scan
      |
      v
Docker Build
      |
      v
Cloud Authentication
      |
      v
Deployment
```

Actions reduce the amount of custom shell scripting required in the workflow.

---

## Important Security Rule

Do not blindly copy an action from the internet.

Always review the action repository, documentation, permissions, maintenance, and version before using it in a production pipeline.
