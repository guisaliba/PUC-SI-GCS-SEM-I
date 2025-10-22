# Merge Strategy

This document describes the merge strategy used in this project. We use **merge commits** as our primary merge strategy to maintain a complete and transparent history of all changes.

## Table of Contents

- [Overview](#overview)
- [Why Merge Commits?](#why-merge-commits)
- [Merge Commit Process](#merge-commit-process)
- [Merge Requirements](#merge-requirements)
- [Best Practices](#best-practices)
- [Comparison with Other Strategies](#comparison-with-other-strategies)
- [Examples](#examples)

## Overview

A **merge commit** is a commit that joins two or more development histories together. When a feature branch is merged into `main`, a new commit is created that has two parents: the latest commit on `main` and the latest commit on the feature branch.

### Key Characteristics

- **Preserves complete history**: All commits from the feature branch are retained
- **Non-destructive**: Original branch history remains intact
- **Explicit merge points**: Clear indication of when features were integrated
- **Traceability**: Easy to track which commits belong to which feature
- **Reversible**: Entire features can be reverted with a single revert

## Why Merge Commits?

### Advantages

1. **Complete History**
   - Every commit from the feature branch is preserved
   - Full context of how features were developed
   - Detailed audit trail for compliance and debugging

2. **Traceability**
   - Easy to see which commits were part of which feature
   - Clear relationship between work items and code changes
   - Simplified debugging and root cause analysis

3. **Collaboration Visibility**
   - Shows the collaborative nature of development
   - Preserves individual contributions
   - Maintains authorship information

4. **Feature Isolation**
   - Each feature branch's commits are grouped together
   - Easy to identify boundaries between features
   - Simplified feature rollback if needed

5. **Easy Reversion**
   - Can revert an entire feature with one command: `git revert -m 1 <merge-commit>`
   - No need to identify individual commits to revert
   - Safe rollback without losing history

### When to Use Merge Commits

✅ **Always use merge commits when:**
- Merging feature branches into `main`
- Merging fix branches into `main`
- Merging any development branch into protected branches
- You want to preserve the complete development history
- Multiple developers collaborated on a feature

## Merge Commit Process

### Step-by-Step Process

1. **Ensure Branch is Ready**
   ```bash
   # Make sure your feature branch is up to date
   git checkout feature/user-authentication
   git fetch origin
   git merge origin/main
   ```

2. **Run Tests Locally**
   ```bash
   # Ensure all tests pass
   npm test
   # or your project's test command
   ```

3. **Push Final Changes**
   ```bash
   git push origin feature/user-authentication
   ```

4. **Create Pull Request**
   - Go to GitHub and create a pull request
   - Fill out the PR template completely
   - Request reviews from team members

5. **Address Review Feedback**
   - Make requested changes
   - Commit changes with conventional commit messages
   - Push updates to the same branch

6. **Final Checks**
   - Ensure all CI checks pass
   - Confirm branch is up to date with `main`
   - Verify minimum approvals are met

7. **Merge via GitHub**
   - Use the "Create a merge commit" option
   - Do NOT use "Squash and merge" or "Rebase and merge"
   - Add a descriptive merge commit message if needed
   - Confirm the merge

8. **Cleanup**
   ```bash
   # Delete the remote branch (usually done automatically by GitHub)
   git push origin --delete feature/user-authentication
   
   # Update your local main
   git checkout main
   git pull origin main
   
   # Delete local branch
   git branch -d feature/user-authentication
   ```

### Merge Commit Message Format

The merge commit message should follow this format:

```
Merge branch '<branch-name>' into main

<Brief description of what the feature/fix accomplishes>

Closes #<issue-number>
```

Example:
```
Merge branch 'feature/user-authentication' into main

Implements user authentication system with login, logout, and 
session management features.

Closes #123
```

## Merge Requirements

Before merging, ensure all requirements are met:

### Pre-Merge Checklist

- [ ] All CI/CD checks pass
- [ ] At least one approving review (or as configured)
- [ ] Branch is up to date with `main`
- [ ] No merge conflicts
- [ ] All review comments addressed
- [ ] Tests added/updated as needed
- [ ] Documentation updated if required
- [ ] No direct commits to `main` (must use PR)

### Automated Checks

These checks must pass before merge:
- Linting
- Unit tests
- Integration tests
- Build process
- Code coverage thresholds (if configured)
- Security scans (if configured)

## Best Practices

### Before Merging

1. **Keep Branches Up to Date**
   ```bash
   git checkout main
   git pull origin main
   git checkout feature/your-branch
   git merge main
   ```
   - Regularly sync with `main` to minimize conflicts
   - Resolve conflicts in your feature branch, not during merge

2. **Clean Commit History**
   - Use meaningful commit messages
   - Follow conventional commits format
   - Each commit should be logical and complete

3. **Test Thoroughly**
   - Run full test suite locally
   - Ensure all new code is tested
   - Verify no regressions in existing functionality

### During Merging

1. **Use GitHub Interface**
   - Always merge through pull requests
   - Never use `git merge` directly on `main` locally
   - Use the "Create a merge commit" button

2. **Verify Merge Settings**
   - Confirm merge commit is selected (not squash or rebase)
   - Review the merge commit message
   - Ensure proper issue references

3. **Document the Merge**
   - Update changelog if maintained
   - Reference related issues/tickets
   - Note any special deployment considerations

### After Merging

1. **Cleanup Branches**
   ```bash
   # Delete merged branches
   git branch -d feature/completed-feature
   git push origin --delete feature/completed-feature
   ```

2. **Update Local Repository**
   ```bash
   git checkout main
   git pull origin main
   ```

3. **Verify Integration**
   - Monitor CI/CD pipelines
   - Check deployment if auto-deployed
   - Verify feature works as expected in integrated state

## Comparison with Other Strategies

### Merge Commit vs Squash Merge

| Aspect | Merge Commit | Squash Merge |
|--------|--------------|--------------|
| History | Preserves all commits | Combines into single commit |
| Traceability | High - see all changes | Low - loses individual commits |
| Reversion | Easy - revert one merge commit | Hard - must revert single squashed commit |
| Graph | Shows branch structure | Linear history |
| Best For | Feature development, collaboration | Small fixes, cleanup |

**Why we chose merge commits:**
- Better traceability for audit and compliance
- Easier to understand feature development
- Simpler to revert entire features
- Preserves collaboration history

### Merge Commit vs Rebase Merge

| Aspect | Merge Commit | Rebase Merge |
|--------|--------------|--------------|
| History | Preserves merge points | Linear, no merge commits |
| Timeline | Actual chronological order | Rewritten timeline |
| Conflicts | Resolve once | May resolve multiple times |
| Reversion | Easy | More complex |
| Best For | Collaborative work | Personal branches |

**Why we chose merge commits:**
- No history rewriting
- Clear merge points
- Safer for collaborative work
- Preserves actual development timeline

## Examples

### Good Merge Commit Workflow

```bash
# 1. Create feature branch
git checkout -b feature/user-profile
git commit -m "feat: add profile page component"
git commit -m "feat: add profile edit functionality"
git commit -m "test: add profile tests"

# 2. Sync with main
git checkout main
git pull origin main
git checkout feature/user-profile
git merge main

# 3. Push and create PR
git push origin feature/user-profile
# Create PR on GitHub

# 4. After approval, merge via GitHub using "Create a merge commit"

# 5. Cleanup
git checkout main
git pull origin main
git branch -d feature/user-profile
```

### History Visualization

After merge commits, history looks like:

```
*   commit abc123 (HEAD -> main)
|\  Merge: def456 ghi789
| | Author: Developer
| | Date: Mon Oct 22 2025
| |
| |     Merge branch 'feature/user-authentication' into main
| |     
| |     Implements user authentication system
| |     
| |     Closes #123
| |
| * commit ghi789
| | Author: Developer
| | Date: Mon Oct 22 2025
| |
| |     test: add authentication tests
| |
| * commit jkl012
| | Author: Developer
| | Date: Mon Oct 22 2025
| |
| |     feat: add authentication service
| |
| * commit mno345
| | Author: Developer
| | Date: Mon Oct 22 2025
| |
| |     feat: add login form
| |
* | commit def456
|/  Author: Another Dev
|   Date: Mon Oct 22 2025
|
|       fix: resolve security issue
|
* commit pqr678
  Author: Developer
  Date: Sun Oct 21 2025

      docs: update readme
```

### Reverting a Feature

If you need to revert an entire feature:

```bash
# Find the merge commit
git log --oneline --merges

# Revert the merge commit (keep main parent with -m 1)
git revert -m 1 abc123

# Push the revert
git push origin main
```

This creates a new commit that undoes all changes from the feature branch while preserving history.

## Troubleshooting

### Merge Conflicts

If conflicts occur:

1. **Don't panic** - conflicts are normal
2. **Resolve in feature branch** before merging to main
3. **Test after resolving** conflicts
4. **Commit the resolution** with a clear message

```bash
git checkout feature/your-branch
git merge main
# Resolve conflicts in your editor
git add .
git commit -m "chore: resolve merge conflicts with main"
git push origin feature/your-branch
```

### Failed Merge

If a merge introduces issues:

1. **Identify the merge commit**
2. **Revert the merge** (see example above)
3. **Fix the issues** in a new branch
4. **Create new PR** with fixes

## Integration with CI/CD

### Pre-Merge Checks

Configure GitHub Actions or your CI/CD system to:
- Run tests on every commit
- Run tests on merge commit (merge preview)
- Block merge if any check fails

### Post-Merge Actions

After successful merge:
- Trigger deployment pipelines
- Update project management tools
- Send notifications to team
- Update documentation sites

## References

- [GitHub Flow Guide](https://guides.github.com/introduction/flow/)
- [Git Merge Documentation](https://git-scm.com/docs/git-merge)
- [Contributing Guidelines](CONTRIBUTING.md)
- [Branching Strategy](BRANCHING_STRATEGY.md)

---

Using merge commits ensures a transparent, traceable, and maintainable development history that supports collaboration and quality assurance.
