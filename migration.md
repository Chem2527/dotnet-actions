Migration Workflow: Bitbucket to GitHub Actions using GitHub CLI
Pre-requisite: install github cli, docker desktop
1. Install GitHub CLI (if not already installed)
Download and install the GitHub CLI for your platform from GitHub CLI Documentation.

2. Install the gh-actions-importer Extension
```bash
gh extension install github/gh-actions-importer
```

3. Verify GitHub CLI Installation
```bash
gh --version
```
4. Authenticate with GitHub
```bash
gh auth login
Select GitHub as the platform.
Authenticate using a browser or a personal access token (PAT).
```
5. Explore the Actions Importer Commands
```bash
gh actions-importer --help
```

6. Update the Actions Importer Tool
Ensure the extension is up-to-date:

```bash
gh actions-importer update
```

7. Generate Required Tokens
```bash
GitHub PAT Token: Create a GitHub Personal Access Token (PAT) with necessary permissions such as repo, workflow, and admin:repo_hook.
Generate GitHub PAT.

Bitbucket Repository Token:

Navigate to Bitbucket's settings.
Generate a new app password with required repository and pipeline permissions.
```

8. Audit Bitbucket Workspaces
Audit your Bitbucket workspace to gather details for migration:

```bash
gh actions-importer audit bitbucket ^
  --workspace fe-be1 ^
  --project-key PROJ ^
  --output-dir "C:/Temp" ^
  --bitbucket-access-token YOUR_BITBUCKET_ACCESS_TOKEN ^
  --github-access-token YOUR_GITHUB_ACCESS_TOKEN
```

9. Check Repository Metrics
Run the forecast command to estimate GitHub Actions usage:

```bash
gh actions-importer forecast bitbucket ^
  --workspace fe-be1 ^
  --output-dir tmp/forecast_reports ^
  --bitbucket-access-token YOUR_BITBUCKET_ACCESS_TOKEN
```
10. Perform a Dry Run
Run a dry-run migration to preview the process without making changes:

```bash
gh actions-importer dry-run bitbucket ^
  --workspace fe-be1 ^
  --repository repo ^
  --output-dir tmp/dry-run ^
  --github-access-token YOUR_GITHUB_ACCESS_TOKEN ^
  --bitbucket-access-token YOUR_BITBUCKET_ACCESS_TOKEN
```
11. Migrate Repository
Migrate your repository from Bitbucket to GitHub:

```bash
gh actions-importer migrate bitbucket ^
  --workspace fe-be1 ^
  --repository demo ^
  --target-url https://github.com/Chem2527/sample-01 ^
  --output-dir tmp/dry-run ^
  --github-access-token YOUR_GITHUB_ACCESS_TOKEN ^
  --bitbucket-access-token YOUR_BITBUCKET_ACCESS_TOKEN
```
