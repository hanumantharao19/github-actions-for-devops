# 10 - Testing and Code Quality

This section teaches how to use GitHub Actions to automatically test application code and perform code-quality checks.

## Learning Objectives

Students will learn:

* Unit testing with pytest
* Running tests using GitHub Actions
* Static code analysis with Pylint
* SonarQube integration
* Quality gates
* Job dependencies using `needs`
* How quality checks fit into CI/CD

## Topics

```text
01-unit-tests
      |
      v
Run automated unit tests
      |
      v
02-pylint
      |
      v
Perform Python code-quality checks
      |
      v
03-sonarqube
      |
      v
Perform deeper code analysis
      |
      v
04-test-and-quality-gate
      |
      v
Combine testing and quality checks
```

## CI Quality Flow

```text
Developer
    |
    | git push
    v
GitHub Repository
    |
    v
GitHub Actions
    |
    +---- Checkout Code
    |
    +---- Install Dependencies
    |
    +---- Run Unit Tests
    |
    +---- Run Pylint
    |
    +---- SonarQube Analysis
    |
    +---- Quality Gate
    |
    v
 PASS / FAIL
```

## CI Principle

The purpose of these checks is to prevent bad-quality code from moving to the next stage of the CI/CD pipeline.

```text
Code
  |
  v
Unit Tests
  |
  +---- FAIL ---> Stop
  |
 PASS
  |
  v
Pylint
  |
  +---- FAIL ---> Stop
  |
 PASS
  |
  v
SonarQube
  |
  +---- FAIL ---> Stop
  |
 PASS
  |
  v
Quality Gate Passed
```

## Folder Structure

```text
10-testing-and-code-quality/
├── README.md
│
├── 01-unit-tests/
│   ├── README.md
│   ├── requirements.txt
│   ├── calculator.py
│   ├── test_calculator.py
│   └── .github/
│       └── workflows/
│           └── unit-tests.yml
│
├── 02-pylint/
│   ├── README.md
│   ├── requirements.txt
│   ├── calculator.py
│   └── .github/
│       └── workflows/
│           └── pylint.yml
│
├── 03-sonarqube/
│   ├── README.md
│   ├── requirements.txt
│   ├── calculator.py
│   ├── sonar-project.properties
│   └── .github/
│       └── workflows/
│           └── sonarqube.yml
│
└── 04-test-and-quality-gate/
    ├── README.md
    ├── requirements.txt
    ├── calculator.py
    ├── test_calculator.py
    ├── sonar-project.properties
    └── .github/
        └── workflows/
            └── quality-gate.yml
```

## Learning Order

Complete the topics in this order:

1. Unit Tests
2. Pylint
3. SonarQube
4. Test and Quality Gate

The final topic combines the concepts learned in the previous topics.
