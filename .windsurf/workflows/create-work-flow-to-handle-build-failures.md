---
description: How to get notifications for failed builds
---

This workflow will guide you on how to update your CI pipeline to automatically notify you when a build fails. We will modify the `.github/workflows/ci.yml` file to add a new job that creates a GitHub Issue whenever the build job fails.

### Steps

1.  **Open the CI Workflow File**:
    Open the `.github/workflows/ci.yml` file in your editor.

2.  **Add a "Notify on Failure" Job**:
    Add the following job to the end of your `ci.yml` file. This job will only run if the `build` job fails.

    ```yaml
    notify_failure:
      needs: build
      if: failure()
      runs-on: ubuntu-latest
      steps:
        - name: Create GitHub Issue on Failure
          uses: actions/github-script@v6
          with:
            script: |
              github.rest.issues.create({
                owner: context.repo.owner,
                repo: context.repo.repo,
                title: `Build failed for commit: ${context.sha}`,
                body: `The build for commit ${context.sha} failed. Please check the Actions tab for more details: https://github.com/${context.repo.owner}/${context.repo.repo}/actions/runs/${context.runId}`
              })
    ```

3.  **Commit and Push the Changes**:
    Save the changes to `.github/workflows/ci.yml`, commit them, and push them to your GitHub repository.

    ```bash
    git add .github/workflows/ci.yml
    git commit -m "feat: Add build failure notifications"
    git push
    ```

Now, whenever the `build` job fails, a new issue will be automatically created in your repository, alerting you to the problem.

