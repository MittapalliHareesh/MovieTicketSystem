---
description: How to run code coverage and linting checks locally
---

This workflow explains how to run the JaCoCo code coverage and Checkstyle linting commands on your local machine. This is useful for verifying your changes before pushing them to GitHub.

### Steps

1.  **Run Maven Verify**:
    Open your terminal and run the following command from the root of your project. The `verify` lifecycle phase is configured in your `pom.xml` to automatically run both Checkstyle and JaCoCo.

    ```bash
    // turbo
    mvn verify
    ```

2.  **View Reports (Optional)**:
    - The **Checkstyle** report can be found at `target/checkstyle-result.xml`.
    - The **JaCoCo** code coverage report can be viewed by opening `target/site/jacoco/index.html` in your browser.

