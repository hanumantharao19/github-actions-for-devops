# Setup Node.js Action

The setup-node action installs and configures Node.js for the workflow runner.

Example:

```yaml
uses: actions/setup-node@v4
```

---

## Why Do We Need It?

Suppose we have a Node.js application.

The CI pipeline needs Node.js before running:

```bash
npm install
npm test
npm run build
```

The workflow can configure Node.js using:

```yaml
- name: Setup Node.js
  uses: actions/setup-node@v4
  with:
    node-version: '20'
```

---

## CI Flow

```text
Checkout
   |
   v
Setup Node.js
   |
   v
npm install
   |
   v
npm test
   |
   v
npm run build
```

---

## `with`

Actions can accept inputs using `with`.

Example:

```yaml
with:
  node-version: '20'
```

The action uses this value to configure the requested Node.js version.

---

## Real-Time Usage

A Node.js application CI pipeline may look like:

```yaml
steps:

  - name: Checkout
    uses: actions/checkout@v4

  - name: Setup Node.js
    uses: actions/setup-node@v4
    with:
      node-version: '20'

  - name: Install dependencies
    run: npm install

  - name: Run tests
    run: npm test

  - name: Build application
    run: npm run build
```
