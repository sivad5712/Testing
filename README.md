# Java Calculator CI/CD Lab

A small Java 21 project used to demonstrate a complete GitHub Actions CI/CD workflow: build, unit test, package a JAR, upload build artifacts, and publish tagged GitHub releases.

## What this repository demonstrates

- Java 21 application development
- Maven build management
- JUnit automated tests
- GitHub Actions continuous integration
- Downloadable workflow artifacts
- Tag-driven GitHub Releases
- CI failure diagnosis and recovery

## Project structure

```text
Testing/
├── .github/workflows/
│   ├── ci.yml
│   └── release.yml
├── src/main/java/com/example/Calculator.java
├── src/test/java/com/example/CalculatorTest.java
├── .gitignore
├── pom.xml
└── README.md
```

## Run locally

Requirements: Java 21+, Maven 3.9+, and Git.

```bash
java -version
mvn -version
mvn clean test
mvn clean verify
```

Run the calculator after packaging:

```bash
java -jar target/java-cicd-demo-1.0.0.jar
```

Expected output:

```text
Addition: 15
Subtraction: 5
Multiplication: 50
Division: 2.5
```

## CI workflow

`.github/workflows/ci.yml` runs on pushes, pull requests, and manual dispatch. It checks out the repository, configures Java 21, runs Maven verification, and uploads the generated JAR as a workflow artifact.

```text
Code push / pull request
        ↓
Checkout repository
        ↓
Set up Java 21
        ↓
Maven clean verify
        ↓
Compile + run tests + package
        ↓
Upload JAR artifact
```

## Release workflow

`.github/workflows/release.yml` runs only when a version tag beginning with `v` is pushed. It rebuilds and tests the tagged source before creating a GitHub Release and attaching the JAR.

Example:

```bash
git tag -a v1.0.0 -m "First calculator release"
git push origin v1.0.0
```

## Test coverage

The unit-test suite verifies:

- Addition
- Subtraction
- Multiplication
- Division
- Division-by-zero validation

## CI failure exercise

To practice diagnosing a failed pipeline, temporarily change the addition assertion in `CalculatorTest.java` from expected `15` to expected `20`, commit it on a separate branch, and open a pull request. The Maven test step should fail with an assertion error. Restore `15` and push again to return the workflow to green.

Do not perform this exercise directly on `main` once branch protection is enabled.

## Recommended repository settings

For a portfolio-quality repository, enable branch protection for `main` and require the CI status check before merging. Also keep release creation restricted to reviewed, passing code.

## Tech stack

Java 21 · Maven · JUnit · GitHub Actions
