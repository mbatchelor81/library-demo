---
description: How to perform a Maven build
---

# Workflow: Performing a Maven Build

This workflow outlines the common steps and commands for building a Java project using Apache Maven.

## Prerequisites

1.  **Java Development Kit (JDK) Installed:** Ensure a compatible JDK version is installed and `JAVA_HOME` environment variable is set.
2.  **Apache Maven Installed:** Ensure Maven is installed and `MAVEN_HOME` (or `M2_HOME`) environment variable is set, and its `bin` directory is in your system's `PATH`.
    *   You can verify by running: `mvn -version`
3.  **`pom.xml` File:** Your project must have a `pom.xml` (Project Object Model) file at its root. This file defines the project's dependencies, build process, plugins, etc.

## Common Maven Build Lifecycle Phases & Commands

Maven builds are based on a lifecycle, and common phases include:

1.  **`mvn clean`**: 
    *   **Purpose:** Deletes the `target` directory (where build artifacts, compiled classes, etc., are stored). This ensures a fresh build.
    *   **Command:**
        ```bash
        // turbo
        mvn clean
        ```

2.  **`mvn validate`**: 
    *   **Purpose:** Validates if the project is correct and all necessary information is available.
    *   **Command:**
        ```bash
        // turbo
        mvn validate
        ```

3.  **`mvn compile`**: 
    *   **Purpose:** Compiles the source code of the project.
    *   **Command:**
        ```bash
        // turbo
        mvn compile
        ```

4.  **`mvn test`**: 
    *   **Purpose:** Runs the tests using a suitable unit testing framework (e.g., JUnit, TestNG). Requires compiled source code (i.e., `compile` phase must have run).
    *   **Command:**
        ```bash
        // turbo
        mvn test
        ```

5.  **`mvn package`**: 
    *   **Purpose:** Takes the compiled code and packages it in its distributable format, such as a JAR, WAR, or EAR file. This runs `compile` and `test` phases first.
    *   **Command:**
        ```bash
        // turbo
        mvn package
        ```

6.  **`mvn verify`**: 
    *   **Purpose:** Runs any checks to verify the package is valid and meets quality criteria.
    *   **Command:**
        ```bash
        // turbo
        mvn verify
        ```

7.  **`mvn install`**: 
    *   **Purpose:** Installs the packaged artifact (e.g., JAR/WAR) into your local Maven repository (`~/.m2/repository`). This makes it available as a dependency for other local projects. This runs all previous phases (`clean`, `compile`, `test`, `package`).
    *   **Command:**
        ```bash
        // turbo
        mvn install
        ```

8.  **`mvn deploy`**: 
    *   **Purpose:** Copies the final package to a remote repository (e.g., Nexus, Artifactory) for sharing with other developers or projects. Requires configuration in `pom.xml` for the remote repository.
    *   **Command:**
        ```bash
        // turbo
        mvn deploy
        ```

## Common Combined Commands

*   **Clean and Package (common for creating a distributable):**
    ```bash
    // turbo
    mvn clean package
    ```
*   **Clean and Install (common for making the artifact available locally):**
    ```bash
    // turbo
    mvn clean install
    ```

## Useful Options

*   **`-DskipTests`**: Skips running tests.
    ```bash
    // turbo
    mvn clean package -DskipTests
    ```
*   **`-P<profile-name>`**: Activates a specific build profile defined in `pom.xml`.
    ```bash
    // turbo
    mvn clean install -Pproduction
    ```
*   **`-o` or `--offline`**: Runs Maven in offline mode (does not try to download dependencies).
    ```bash
    // turbo
    mvn package -o
    ```
*   **`-U` or `--update-snapshots`**: Forces Maven to check for updated releases and snapshots on remote repositories.
    ```bash
    // turbo
    mvn clean install -U
    ```
*   **`-X` or `--debug`**: Produces execution debug output.
    ```bash
    // turbo
    mvn compile -X
    ```

## Troubleshooting

*   **Dependency Issues:** Check your `pom.xml` for correct dependency declarations. Ensure repositories are accessible.
*   **Compilation Errors:** Review the compiler output for specific error messages.
*   **Test Failures:** Examine test reports usually found in `target/surefire-reports`.

This workflow provides a foundational understanding of Maven builds. Refer to the official Apache Maven documentation for more advanced topics and plugin configurations.
