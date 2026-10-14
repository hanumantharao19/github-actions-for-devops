# 02 - Node.js CI

## Objective

Build a Continuous Integration pipeline for a Node.js application.

## CI Flow

```text
GitHub
   |
   v
Checkout
   |
   v
Setup Node.js
   |
   v
Install Dependencies
   |
   v
Run Tests
   |
   v
Build Application
   |
   v
CI Passed
```

## npm Commands

### Install dependencies

```bash
npm ci
```

### Run tests

```bash
npm test
```

### Build application

```bash
npm run build
```

## Why `npm ci`?

`npm ci` is commonly used in CI environments because it installs dependencies from the lock file in a clean and reproducible way.

## Real-Time DevOps Flow

```text
Developer
    |
    v
Pull Request
    |
    v
GitHub Actions
    |
    ├── npm ci
    ├── npm test
    └── npm run build
            |
            v
         CI Passed
```

## Key Learning

This is the same CI pattern used for Python:

```text
Checkout
   ↓
Setup Runtime
   ↓
Install Dependencies
   ↓
Test
   ↓
Build
```

Only the application ecosystem changes.
