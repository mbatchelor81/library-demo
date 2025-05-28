---
description: How to set up a repository for debugging
---

# Workflow: Setting Up a Repository for Debugging

This workflow outlines the steps to prepare your local repository for an effective debugging session.

1.  **Ensure Your Code is Up-to-Date:**
    *   Pull the latest changes from the remote repository for the relevant branch:
        ```bash
        git pull origin <branch-name>
        ```
    *   Ensure your working directory is clean (no uncommitted changes that might interfere).

2.  **Set Up a Clean Environment (if applicable):
    *   **Python:** Activate your virtual environment.
        ```bash
        source .venv/bin/activate
        ```
    *   **Node.js:** Ensure correct Node version (e.g., using `nvm`).
        ```bash
        nvm use
        ```
    *   **Java/Maven:** Ensure your `JAVA_HOME` and `MAVEN_HOME` are set correctly.

3.  **Install/Update Dependencies:**
    *   Make sure all project dependencies are installed and at their correct versions.
        *   Python: `pip install -r requirements.txt` or `poetry install`
        *   Node.js: `npm install` or `yarn install`
        *   Maven: Maven handles this automatically during build, but you can run `mvn dependency:resolve`

4.  **Identify a Minimal Reproducible Example:**
    *   Try to isolate the bug with the smallest amount of code or the simplest set of steps possible.

5.  **Configure Debugging Tools:**
    *   **IDE Debugger:** Set breakpoints in your IDE (e.g., VS Code, IntelliJ) at relevant points in the code.
    *   **Logging:** Add detailed logging statements around the suspected problematic code sections. Use different log levels (DEBUG, INFO, ERROR) appropriately.
        *   Example (Python):
            ```python
            import logging
            logging.basicConfig(level=logging.DEBUG)
            logger = logging.getLogger(__name__)

            def my_function(param):
                logger.debug(f"Function called with param: {param}")
                # ... rest of the code ...
            ```

6.  **Run the Code with the Debugger Attached or Logging Enabled:**
    *   Execute the specific part of the application that triggers the bug.
    *   Step through the code, inspect variable values, and observe the program flow.

7.  **Check External Services & Configurations:**
    *   If your application interacts with databases, APIs, or other services, ensure they are running and accessible.
    *   Verify configuration files (`.env`, `config.json`, etc.) have the correct settings for your debugging environment.
