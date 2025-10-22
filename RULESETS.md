# GitHub Rulesets Configuration

This document describes the GitHub rulesets configured for this repository to enforce code quality and commit standards.

## Existing Rulesets

### Production Ruleset
- **Name**: `production-ruleset`
- **Target Branches**: 
  - `main`
  - `release/**/*`
- **Purpose**: Protects production branches with standard branch protection rules

## Commit Metadata Enforcement Ruleset

### Overview
To ensure proper commit tracking and accountability, a new ruleset enforces that all commits must include valid author metadata (name and email).

### Ruleset Configuration

#### Ruleset Name
`commit-metadata-ruleset`

#### Target Branches
- `main`
- `release/**`

#### Rules Applied
1. **Require commit metadata validation** - Enforced via GitHub Actions workflow
   - Author name must be non-empty
   - Author email must be valid format (e.g., `user@example.com`)

### Implementation Details

#### Automated Validation
The enforcement is implemented through:

1. **GitHub Actions Workflow** (`.github/workflows/commit-metadata-validation.yml`)
   - Runs on push and pull request events to protected branches
   - Validates all commits in the push/PR
   - Fails if any commit has missing or invalid author metadata

2. **Pre-commit Hook** (Optional, for local validation)
   - Can be installed locally to catch issues before pushing
   - Located at `.github/hooks/pre-commit`

### How to Configure in GitHub UI

To create this ruleset in GitHub:

1. Navigate to your repository on GitHub
2. Go to **Settings** → **Rules** → **Rulesets**
3. Click **New ruleset** → **New branch ruleset**
4. Configure the ruleset:
   - **Ruleset name**: `commit-metadata-ruleset`
   - **Enforcement status**: Active
   - **Target branches**: Add `main` and `release/**`
   - **Rules**:
     - ✅ Require status checks to pass before merging
       - Add status check: `Validate Commit Author Metadata`
     - ✅ Require branches to be up to date before merging
     - ✅ Block force pushes

5. Click **Create** to save the ruleset

### For Developers

#### Setting Up Git Configuration
Ensure your local git configuration includes your name and email:

```bash
# Set globally (for all repositories)
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# Or set per repository
git config user.name "Your Name"
git config user.email "your.email@example.com"

# Verify configuration
git config user.name
git config user.email
```

#### Installing Pre-commit Hook (Optional)
To validate commits locally before pushing:

```bash
# From repository root
cp .github/hooks/pre-commit .git/hooks/pre-commit
chmod +x .git/hooks/pre-commit
```

### Validation Details

The workflow validates:
- ✅ Author name is not empty
- ✅ Author email is not empty
- ✅ Author email follows valid email format (contains @ and domain)

### Troubleshooting

#### My commits are being rejected
1. Check your git configuration:
   ```bash
   git config user.name
   git config user.email
   ```

2. If not set, configure them:
   ```bash
   git config user.name "Your Name"
   git config user.email "your.email@example.com"
   ```

3. If you've already made commits with invalid metadata:
   ```bash
   # Amend the last commit
   git commit --amend --author="Your Name <your.email@example.com>"
   
   # For older commits, use interactive rebase
   git rebase -i HEAD~N  # where N is the number of commits to go back
   ```

#### The workflow is not running
- Ensure the workflow file is in `.github/workflows/` directory
- Check that the branch is targeted by the ruleset (main or release/**)
- Verify the workflow is enabled in repository settings

### Benefits

1. **Accountability**: Every commit is properly attributed to its author
2. **Audit Trail**: Clear history of who made what changes
3. **Compliance**: Meets organizational requirements for code tracking
4. **Integration**: Works with existing tooling and git workflows

### Related Documentation
- [GitHub Rulesets Documentation](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets)
- [Git Configuration](https://git-scm.com/book/en/v2/Customizing-Git-Git-Configuration)
