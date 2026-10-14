# 03 - Java CI

## Objective

Build a Continuous Integration pipeline for a Java Maven application.

## CI Flow

```text
GitHub
   |
   v
Checkout
   |
   v
Setup Java
   |
   v
Maven Build
   |
   v
Unit Tests
   |
   v
Package
   |
   v
CI Passed
```

## Maven

Maven is commonly used to:

* Manage Java dependencies
* Compile Java code
* Run tests
* Package applications

## Important Commands

```bash
mvn test
```

Runs tests.

```bash
mvn package
```

Builds and packages the application.

## GitHub Actions Flow

```text
actions/checkout
        |
        v
actions/setup-java
        |
        v
mvn test
        |
        v
mvn package
```

## Real-Time DevOps Example

A Java Spring Boot application can use the same CI pattern:

```text
Developer
    |
    v
Pull Request
    |
    v
GitHub Actions
    |
    ├── Checkout
    ├── Setup Java
    ├── Maven Test
    └── Maven Package
            |
            v
       Build Artifact
```

Later, the generated JAR can be uploaded as a GitHub Actions artifact and deployed.
