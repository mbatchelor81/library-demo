---
description: How to create a Pull Request via API with description guidelines
---

# Workflow: Creating a Pull Request via API

This workflow describes how to create a Pull Request (PR) using a generic API (e.g., GitHub, GitLab, Bitbucket API) and includes guidelines for writing a good PR description.

## Prerequisites

1.  **API Access Token:** Obtain a personal access token with the necessary scopes (e.g., `repo` for GitHub).
2.  **Repository Information:**
    *   Owner/Organization name
    *   Repository name
3.  **Branch Names:**
    *   `head`: The name of the branch where your changes are implemented.
    *   `base`: The name of the branch you want to merge your changes into (e.g., `main`, `develop`).

## API Request (Example: GitHub API)

*   **Endpoint:** `POST /repos/{owner}/{repo}/pulls`
*   **Headers:**
    *   `Accept: application/vnd.github.v3+json`
    *   `Authorization: token YOUR_ACCESS_TOKEN`
*   **Request Body (JSON):**
    ```json
    {
      "title": "Your PR Title: A brief summary of changes",
      "head": "your-feature-branch",
      "base": "main",
      "body": "Detailed description of the PR (see guidelines below)",
      "draft": false, // Optional: set to true to create a draft PR
      "maintainer_can_modify": true // Optional: allow maintainers to push to your branch
    }
    ```

## PR Description Guidelines

A well-written PR description helps reviewers understand the changes and speeds up the review process.

```markdown
### 📝 Purpose

<!-- Clearly describe the problem this PR solves or the feature it implements. -->
<!-- Link to any relevant issues, e.g., "Fixes #123" or "Implements JIRA-456". -->

### Changes Made

<!-- Provide a concise summary of the changes. Bullet points are often effective. -->
<!-- - Added new X component
- Modified Y service to support Z
- Refactored A module for better performance -->

### How to Test

<!-- Provide clear, step-by-step instructions on how to test these changes. -->
<!-- 1. Check out this branch.
2. Run `npm install` and `npm start`.
3. Navigate to `/new-feature-page`.
4. Verify that X behaves as expected when Y condition is met. -->

### Screenshots/GIFs (if applicable)

<!-- If the changes affect the UI, include screenshots or GIFs to showcase the before/after or the new functionality. -->

### Checklist

<!-- Optional: A self-review checklist. -->
- [ ] Code follows project coding standards.
- [ ] Unit tests have been added/updated.
- [ ] Integration tests have been added/updated (if applicable).
- [ ] Documentation has been updated (if applicable).
- [ ] All automated checks (linters, tests) pass.

### Additional Notes (if any)

<!-- Any other relevant information, considerations, or known issues. -->
```

## Example API Call (using `curl` for GitHub)

```bash
curl \
  -X POST \
  -H "Accept: application/vnd.github.v3+json" \
  -H "Authorization: token YOUR_GITHUB_TOKEN" \
  https://api.github.com/repos/OWNER/REPO/pulls \
  -d '{
    "title":"Add new login feature",
    "body":"This PR introduces a new login mechanism using OAuth2. Addresses issue #42.\n\n### Changes Made\n- Added OAuth2 client library.\n- Implemented /auth/login endpoint.\n- Updated user model to store OAuth tokens.\n\n### How to Test\n1. Run the application.\n2. Navigate to /login.\n3. Click \"Login with Provider\".\n4. Verify successful authentication and redirection.",
    "head":"feature/oauth-login",
    "base":"develop"
  }'
```

Remember to replace `YOUR_GITHUB_TOKEN`, `OWNER`, `REPO`, branch names, and other details with your actual information.
