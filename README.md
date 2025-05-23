# CI/CD Pipeline with GitHub Actions for Maven/Gradle Project

## Overview

This project demonstrates how to:

* Create a CI/CD pipeline using **GitHub Actions** for a Maven or Gradle-based Java project.
* Integrate a source code repository from **GitHub**.
* Automatically build the project upon each push or pull request.
* Run unit tests and generate test reports.
* Ensure code quality and streamlined integration through automation.

## Prerequisites

Before setting up this pipeline, ensure the following:

* A Java project using Maven or Gradle is available in a GitHub repository.
* The project contains a valid `pom.xml` (for Maven) or `build.gradle` (for Gradle).
* Basic familiarity with GitHub Actions and workflow syntax.

## Project Structure

For Maven:

```
Javateam/
├── pom.xml
└── src/
    ├── main/java/...
    └── test/java/...

```


## Step 1: Setting Up the GitHub Actions Workflow

1. Inside the root of your GitHub repository, create the following directory structure:

```
.github/
└── workflows/
    └── main.yml
```

2. Example GitHub Actions Workflow for Maven:

```yaml
name: Java CI with Maven

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Code
        uses: actions/checkout@v3

      - name: Set up JDK 17
        uses: actions/setup-java@v3
        with:
          java-version: '17'
          distribution: 'temurin'

      - name: Build with Maven
        run: mvn clean install

      - name: Archive Test Reports
        if: always()
        uses: actions/upload-artifact@v3
        with:
          name: test-reports
          path: target/surefire-reports/
```

## Step 2: Push Code and Trigger Workflow

* Commit and push your code to the `main` branch.
* GitHub Actions will automatically trigger the build pipeline.
* Monitor the status under the "Actions" tab of your GitHub repository.

## Step 3: View Test Reports

* Navigate to the specific workflow run.
* Download the `test-reports` artifact to view your unit test results.

## Additional Notes

* You can add steps for code coverage tools like **Jacoco** or **SonarCloud**.
* Notifications (Slack, Email, etc.) can be added using marketplace actions.
* Consider adding deployment jobs to cloud services (Azure, AWS, etc.) after build.

---
