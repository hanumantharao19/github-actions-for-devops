# 01 - Python CI

## Objective

Build a Continuous Integration pipeline for a Python application using GitHub Actions.

## CI Flow

```text
GitHub Push
     |
     v
Checkout Code
     |
     v
Setup Python
     |
     v
Install Dependencies
     |
     v
Run Tests
     |
     v
CI Passed
```

## Files

```text
01-python-ci/
├── README.md
├── requirements.txt
└── .github/workflows/
    └── python-ci.yml
```

## Key GitHub Actions

We will use:

```yaml
actions/checkout
actions/setup-python
```

## Important Steps

### 1. Checkout

Downloads the repository code to the runner.

### 2. Setup Python

Installs/configures Python on the runner.

### 3. Install Dependencies

Installs Python packages from `requirements.txt`.

### 4. Run Tests

Runs the application's automated tests.

## Real-Time Example

For a Python service:

```text
Developer
   |
   | Push
   v
GitHub
   |
   v
GitHub Actions
   |
   ├── Checkout
   ├── Setup Python
   ├── pip install
   └── pytest
          |
          v
      CI Result
```

## Important

The purpose of CI is to detect problems **before code is merged or deployed**.
