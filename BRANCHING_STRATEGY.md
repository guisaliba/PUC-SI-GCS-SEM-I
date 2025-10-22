# Branching Strategy

This document describes the branching strategy used in this project. We follow **GitHub Flow** combined with **conventional branch naming** to maintain a clean and organized repository.

## Table of Contents

- [Overview](#overview)
- [GitHub Flow](#github-flow)
- [Branch Types](#branch-types)
- [Branch Naming Convention](#branch-naming-convention)
- [Workflow](#workflow)
- [Best Practices](#best-practices)
- [Examples](#examples)

## Overview

Our branching strategy is designed to:
- Keep the `main` branch always deployable
- Enable parallel development
- Support continuous integration and deployment
- Maintain a clean and understandable history
- Facilitate code review and collaboration

## GitHub Flow

GitHub Flow is a lightweight, branch-based workflow that supports teams and projects with regular deployments.

### Core Principles

1. **Main branch is always deployable**: The `main` branch contains production-ready code
2. **Create descriptive branches**: All work happens in feature branches created from `main`
3. **Commit often**: Regular commits with clear messages following conventional commits
4. **Open pull requests early**: Get feedback early and often
5. **Merge after review**: Merge to `main` only after approval and passing all checks
6. **Deploy immediately**: Once merged to `main`, changes can be deployed

### Workflow Diagram

```
main (protected)
  |
  |-- feature/user-authentication (create branch)
  |     |
  |     |-- commit: feat: add login form
  |     |-- commit: feat: add authentication service
  |     |-- commit: test: add auth tests
  |     |
  |     |-- PR created and reviewed
  |     |
  |-- merge (via merge commit)
  |
  |-- feature/user-profile (create branch)
        |
        |-- commit: feat: create profile page
        |-- ...
```

## Branch Types

We use conventional branch prefixes to indicate the purpose of each branch:

### 1. Main Branch

- **Name**: `main`
- **Purpose**: Production-ready code
- **Protection**: Protected branch with strict rules (see [BRANCH_PROTECTION.md](BRANCH_PROTECTION.md))
- **Lifetime**: Permanent
- **Who can merge**: Maintainers after PR approval

### 2. Feature Branches

- **Prefix**: `feature/`
- **Purpose**: New features or enhancements
- **Created from**: `main`
- **Merged into**: `main`
- **Lifetime**: Temporary (deleted after merge)

### 3. Fix Branches

- **Prefix**: `fix/` or `bugfix/`
- **Purpose**: Bug fixes
- **Created from**: `main`
- **Merged into**: `main`
- **Lifetime**: Temporary (deleted after merge)

### 4. Hotfix Branches

- **Prefix**: `hotfix/`
- **Purpose**: Critical production bug fixes that need immediate attention
- **Created from**: `main`
- **Merged into**: `main`
- **Lifetime**: Temporary (deleted after merge)

### 5. Documentation Branches

- **Prefix**: `docs/`
- **Purpose**: Documentation updates and improvements
- **Created from**: `main`
- **Merged into**: `main`
- **Lifetime**: Temporary (deleted after merge)

### 6. Refactoring Branches

- **Prefix**: `refactor/`
- **Purpose**: Code refactoring without changing functionality
- **Created from**: `main`
- **Merged into**: `main`
- **Lifetime**: Temporary (deleted after merge)

### 7. Chore Branches

- **Prefix**: `chore/`
- **Purpose**: Maintenance tasks, dependency updates, build changes
- **Created from**: `main`
- **Merged into**: `main`
- **Lifetime**: Temporary (deleted after merge)

### 8. Test Branches

- **Prefix**: `test/`
- **Purpose**: Adding or updating tests
- **Created from**: `main`
- **Merged into**: `main`
- **Lifetime**: Temporary (deleted after merge)

## Branch Naming Convention

### Format

```
<type>/<short-description>
```

### Rules

1. **Use lowercase letters only**
2. **Use hyphens to separate words** (no spaces or underscores)
3. **Keep it short and descriptive** (ideally under 50 characters)
4. **Use present tense imperative mood** (e.g., "add" not "adding" or "added")
5. **Be specific about what the branch does**

### Pattern

```
<type>/<issue-number>-<brief-description>
```

Including the issue number (when applicable) helps track work:

```
feature/123-user-authentication
fix/456-login-error
docs/789-update-readme
```

## Workflow

### Creating a Branch

1. **Update your local main branch:**
   ```bash
   git checkout main
   git pull origin main
   ```

2. **Create and switch to a new branch:**
   ```bash
   git checkout -b feature/user-authentication
   ```

### Working on a Branch

1. **Make changes and commit regularly:**
   ```bash
   git add .
   git commit -m "feat: add login form component"
   ```

2. **Push your branch to remote:**
   ```bash
   git push origin feature/user-authentication
   ```

3. **Keep your branch up to date with main:**
   ```bash
   git checkout main
   git pull origin main
   git checkout feature/user-authentication
   git merge main
   ```

### Creating a Pull Request

1. **Push all commits to your branch**
2. **Open a pull request on GitHub**
3. **Fill out the PR template completely**
4. **Request reviews from team members**
5. **Address feedback and make requested changes**

### Merging

1. **Ensure all CI checks pass**
2. **Obtain required approvals** (minimum 1 reviewer)
3. **Update branch with latest main** (if needed)
4. **Merge using merge commit** (no squash or rebase)
5. **Delete the branch after merge**

## Best Practices

### Do's ✅

- **Create a new branch for each feature or fix**
- **Keep branches short-lived** (aim for < 3 days)
- **Commit often with meaningful messages**
- **Keep branch scope focused** (one feature/fix per branch)
- **Regularly sync with main** to avoid large merge conflicts
- **Write descriptive branch names** that explain the purpose
- **Delete branches after merging** to keep repository clean
- **Test thoroughly before creating PR**
- **Update documentation** in the same branch as code changes

### Don'ts ❌

- **Don't commit directly to main** (use pull requests)
- **Don't create overly broad branches** (keep scope limited)
- **Don't let branches live for too long** (increases merge conflicts)
- **Don't use generic names** like `my-branch` or `temp`
- **Don't force push to shared branches** (unless absolutely necessary)
- **Don't merge without approval and passing tests**
- **Don't reuse branches** (create fresh branches for new work)
- **Don't work on multiple unrelated features** in one branch

### Branch Hygiene

- **Review your changes** before creating a PR
- **Resolve merge conflicts** promptly
- **Remove obsolete branches** regularly
- **Keep commit history clean** with meaningful messages
- **Update branch descriptions** if scope changes

## Examples

### Good Branch Names ✅

```
feature/user-authentication
feature/123-payment-integration
fix/login-redirect-issue
fix/456-null-pointer-exception
hotfix/critical-security-vulnerability
docs/update-api-documentation
docs/789-contributing-guidelines
refactor/database-connection-pool
chore/update-dependencies
chore/101-upgrade-nodejs
test/add-authentication-tests
```

### Bad Branch Names ❌

```
my-branch                    # Not descriptive
temp                         # Not descriptive
feature                      # Missing description
Fix_Login_Bug               # Wrong case, underscores
feature/add-user-auth-and-profile-and-settings  # Too broad
john-working                 # Personal, not descriptive
test123                      # Not meaningful
```

### Branch Lifetime Example

```bash
# Day 1: Create and start work
git checkout -b feature/user-authentication
git commit -m "feat: add login form"
git commit -m "feat: add authentication service"
git push origin feature/user-authentication

# Day 2: Continue work, sync with main
git checkout main && git pull
git checkout feature/user-authentication
git merge main
git commit -m "test: add authentication tests"
git push origin feature/user-authentication

# Day 2: Create PR and get review
# Open PR, address feedback

# Day 3: Merge and cleanup
# PR approved and merged via GitHub
git checkout main
git pull origin main
git branch -d feature/user-authentication
git push origin --delete feature/user-authentication
```

## Integration with Other Practices

### Conventional Commits

Branch names should align with commit message types:
- `feature/` branches → `feat:` commits
- `fix/` branches → `fix:` commits
- `docs/` branches → `docs:` commits

See [CONTRIBUTING.md](CONTRIBUTING.md) for commit message guidelines.

### Semantic Versioning

Feature and fix branches help determine version bumps:
- `feature/` branches → Minor version bump (0.X.0)
- `fix/` branches → Patch version bump (0.0.X)
- Breaking changes → Major version bump (X.0.0)

See [VERSIONING.md](VERSIONING.md) for versioning details.

## Troubleshooting

### Merge Conflicts

If you encounter merge conflicts:

1. **Pull latest main:**
   ```bash
   git checkout main
   git pull origin main
   ```

2. **Merge main into your branch:**
   ```bash
   git checkout feature/your-branch
   git merge main
   ```

3. **Resolve conflicts** in your editor

4. **Complete the merge:**
   ```bash
   git add .
   git commit -m "chore: resolve merge conflicts with main"
   git push origin feature/your-branch
   ```

### Accidental Commit to Main

If you accidentally commit to `main`:

1. **Create a new branch with your changes:**
   ```bash
   git branch feature/rescue-commits
   ```

2. **Reset main to match origin:**
   ```bash
   git reset --hard origin/main
   ```

3. **Switch to your new branch:**
   ```bash
   git checkout feature/rescue-commits
   ```

4. **Create a proper PR** from the new branch

## References

- [GitHub Flow Guide](https://guides.github.com/introduction/flow/)
- [Contributing Guidelines](CONTRIBUTING.md)
- [Merge Strategy](MERGE_STRATEGY.md)
- [Branch Protection Rules](BRANCH_PROTECTION.md)

---

Following this branching strategy ensures a clean, organized, and collaborative development process.
