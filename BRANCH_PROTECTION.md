# Branch Protection Rules

This document describes the branch protection rules and requirements for this repository. These rules help maintain code quality, prevent accidental changes, and ensure proper review processes.

## Table of Contents

- [Overview](#overview)
- [Protected Branches](#protected-branches)
- [Main Branch Protection Rules](#main-branch-protection-rules)
- [Rule Implementation](#rule-implementation)
- [Enforcement](#enforcement)
- [Exceptions](#exceptions)
- [Troubleshooting](#troubleshooting)

## Overview

Branch protection rules are safeguards that prevent accidental or unauthorized changes to important branches in the repository. These rules enforce our development workflow and quality standards.

### Why Branch Protection?

- **Prevent accidental commits**: No direct commits to protected branches
- **Enforce code review**: Require pull request reviews before merging
- **Maintain quality**: Ensure tests pass before merging
- **Preserve history**: Prevent force pushes and branch deletion
- **Enable collaboration**: Ensure multiple eyes on every change

## Protected Branches

### Main Branch

The `main` branch is the primary protected branch containing production-ready code.

**Status**: Protected ✅

**Purpose**: 
- Contains stable, production-ready code
- Always in a deployable state
- Source of truth for all development

## Main Branch Protection Rules

### 1. Require Pull Request Reviews Before Merging

**Status**: ✅ REQUIRED

**Configuration**:
- **Minimum number of approving reviews**: 1
- **Dismiss stale reviews**: Recommended (when new commits are pushed)
- **Require review from code owners**: Optional (if CODEOWNERS file exists)

**What this means**:
- All changes must go through a pull request
- At least one team member must review and approve
- Approval can be dismissed if new changes are pushed

**Example Workflow**:
```bash
# ❌ This is blocked
git checkout main
git commit -m "fix: update code"
git push origin main  # BLOCKED by branch protection

# ✅ This is the correct way
git checkout -b fix/update-code
git commit -m "fix: update code"
git push origin fix/update-code
# Create PR on GitHub, get review, then merge
```

### 2. Require Status Checks Before Merging

**Status**: ✅ REQUIRED (when CI is configured)

**Configuration**:
- All CI checks must pass
- Tests must pass
- Linting must pass
- Build must succeed

**Required Checks** (when configured):
- ✅ Unit tests
- ✅ Integration tests
- ✅ Linting checks
- ✅ Build verification
- ✅ Security scans (if configured)

**What this means**:
- PRs cannot be merged if any check fails
- All tests must pass before approval
- Automated quality gates enforce standards

### 3. Require Branches to be Up to Date Before Merging

**Status**: ✅ REQUIRED

**Configuration**:
- Branch must be up to date with `main`
- Must include latest changes from base branch

**What this means**:
- Before merging, your branch must include latest `main` changes
- Prevents integration issues
- Ensures tests run against current codebase

**How to keep up to date**:
```bash
# Method 1: Merge main into your branch
git checkout feature/your-branch
git fetch origin
git merge origin/main
git push origin feature/your-branch

# Method 2: Use GitHub's "Update branch" button in PR
```

### 4. Require Linear History (Optional)

**Status**: ⚪ OPTIONAL

**Our Setting**: Disabled (we use merge commits)

**What this means**:
- We allow merge commits (non-linear history)
- Feature branch commits are preserved
- Merge commits show integration points

See [MERGE_STRATEGY.md](MERGE_STRATEGY.md) for details.

### 5. Do Not Allow Force Pushes

**Status**: ✅ ENFORCED

**Configuration**:
- Force pushes are blocked on `main`
- Protects against history rewriting

**What this means**:
```bash
# ❌ This is blocked on main
git push --force origin main

# ✅ Force push allowed on feature branches (with caution)
git push --force origin feature/your-branch
```

**Important**: While force pushing is blocked on `main`, it's allowed on feature branches. Use with extreme caution, especially on shared branches.

### 6. Do Not Allow Deletions

**Status**: ✅ ENFORCED

**Configuration**:
- Branch deletion is blocked
- `main` branch cannot be deleted

**What this means**:
```bash
# ❌ This is blocked
git push origin --delete main

# ✅ Feature branches can be deleted after merge
git push origin --delete feature/merged-feature
```

### 7. Require Signed Commits (Optional)

**Status**: ⚪ OPTIONAL

**Configuration**: Can be enabled for additional security

**What this means**:
- Commits must be signed with GPG/SSH key
- Verifies commit author identity
- Additional security layer

**How to sign commits**:
```bash
# Configure GPG signing
git config --global user.signingkey YOUR_KEY_ID
git config --global commit.gpgsign true

# Sign individual commit
git commit -S -m "feat: add feature"
```

### 8. Include Administrators

**Status**: ✅ ENFORCED

**Configuration**:
- Rules apply to administrators too
- No exceptions for repository admins

**What this means**:
- Even repository administrators must follow the rules
- Creates PR, get review, pass checks
- Ensures consistent quality standards

## Rule Implementation

### Setting Up Branch Protection (For Administrators)

Branch protection rules are configured in GitHub repository settings:

1. **Navigate to Settings**:
   - Go to repository on GitHub
   - Click "Settings" tab
   - Select "Branches" from sidebar

2. **Add Branch Protection Rule**:
   - Click "Add rule"
   - Enter branch name pattern: `main`

3. **Configure Protection Rules**:
   - ✅ Require a pull request before merging
     - ✅ Require approvals (minimum: 1)
     - ✅ Dismiss stale pull request approvals when new commits are pushed
   - ✅ Require status checks to pass before merging
     - ✅ Require branches to be up to date before merging
     - Select required checks (if CI configured)
   - ✅ Do not allow bypassing the above settings
   - ✅ Restrict who can push to matching branches (optional)
   - ✅ Allow force pushes: Disabled
   - ✅ Allow deletions: Disabled

4. **Save Changes**:
   - Click "Create" or "Save changes"

### Visual Reference

```
Repository Settings → Branches → Add rule

Branch name pattern: main

[✓] Require a pull request before merging
    [✓] Require approvals: 1
    [✓] Dismiss stale pull request approvals when new commits are pushed
    [ ] Require review from Code Owners (optional)

[✓] Require status checks to pass before merging
    [✓] Require branches to be up to date before merging
    Required status checks:
    - [ ] tests
    - [ ] lint
    - [ ] build

[✓] Do not allow bypassing the above settings

[ ] Restrict who can push to matching branches

[ ] Allow force pushes

[ ] Allow deletions

[✓] Include administrators
```

## Enforcement

### What Happens When Rules Are Violated?

1. **Direct Push to Main**:
   ```
   remote: error: GH006: Protected branch update failed
   remote: error: Cannot push to protected branch 'main'
   To github.com:user/repo.git
   ! [remote rejected] main -> main (protected branch hook declined)
   ```

2. **Merge Without Approval**:
   - GitHub prevents merge button from being clicked
   - Shows "Review required" status
   - Lists which requirements are not met

3. **Merge with Failing Tests**:
   - Merge button is disabled
   - Shows "Some checks were not successful"
   - Lists failing checks

4. **Merge with Outdated Branch**:
   - GitHub shows "This branch is out-of-date with the base branch"
   - Requires update before merge
   - "Update branch" button available

### Bypassing Rules (Administrators Only)

While administrators can technically bypass rules, it should be avoided:

**When bypass might be acceptable**:
- Emergency hotfixes in critical situations
- Automated tooling requirements
- Repository maintenance tasks

**Process for bypass**:
1. Document the reason
2. Get team consensus
3. Create issue explaining the bypass
4. Perform the action
5. Immediately create PR to fix properly

## Exceptions

### Temporary Exceptions

In rare cases, temporary exceptions may be needed:

**Valid Reasons**:
- Critical security hotfix
- System outage requiring immediate fix
- Broken CI/CD that blocks all merges

**Process**:
1. Document the issue
2. Get approval from team lead
3. Temporarily disable specific rule
4. Make the fix
5. Re-enable the rule immediately
6. Follow up with proper PR for documentation

### Auto-merge Bots

If using automated tools (e.g., Dependabot):

**Configuration**:
- Bot must follow same rules
- Consider auto-approval for trusted updates
- Monitor automated PRs regularly

## Troubleshooting

### "Changes requested" - Can't Merge

**Solution**:
- Address reviewer's feedback
- Push new commits with fixes
- Request re-review
- Wait for approval

### "Checks Failed" - Can't Merge

**Solution**:
```bash
# Fix the issues locally
npm test  # or your test command
npm run lint  # fix linting issues

# Commit fixes
git add .
git commit -m "fix: resolve test failures"
git push origin feature/your-branch
```

### "Branch out of date" - Can't Merge

**Solution**:
```bash
# Option 1: Merge main into your branch
git checkout feature/your-branch
git fetch origin
git merge origin/main
# Resolve any conflicts
git push origin feature/your-branch

# Option 2: Use GitHub's "Update branch" button
```

### "No approval" - Can't Merge

**Solution**:
- Request review from team members
- Address any feedback
- Wait for approval
- Check that required reviewers have approved

### Force Push Blocked

**Error**:
```
! [remote rejected] main -> main (protected branch hook declined)
```

**Solution**:
- Don't force push to `main`
- Use pull request workflow
- Force push only to feature branches if absolutely needed

## Best Practices

### For Contributors

1. **Always use feature branches**
   - Never work directly on `main`
   - Create descriptive branches

2. **Keep branches up to date**
   - Regularly merge `main` into your branch
   - Resolve conflicts early

3. **Request reviews early**
   - Open PR early for feedback
   - Don't wait until work is complete

4. **Respond to feedback**
   - Address review comments promptly
   - Ask questions if unclear

### For Reviewers

1. **Review promptly**
   - Aim to review within 24-48 hours
   - Don't block team progress

2. **Be constructive**
   - Focus on code quality
   - Suggest improvements clearly

3. **Use review features**
   - Approve when satisfied
   - Request changes when needed
   - Comment for questions

### For Administrators

1. **Enforce rules consistently**
   - Apply to everyone equally
   - Document any exceptions

2. **Monitor compliance**
   - Review merge patterns
   - Ensure rules are effective

3. **Update rules as needed**
   - Adapt to team needs
   - Document changes

## Verification

### How to Verify Rules Are Active

1. **Check in GitHub UI**:
   - Go to Settings → Branches
   - Verify rule exists for `main`
   - Check all settings are enabled

2. **Test with Pull Request**:
   - Create test PR
   - Verify approval required
   - Check status checks required
   - Confirm merge button disabled until requirements met

3. **Test Direct Push** (will fail):
   ```bash
   git checkout main
   echo "test" >> test.txt
   git add test.txt
   git commit -m "test"
   git push origin main  # Should be blocked
   ```

## Related Documentation

- [Contributing Guidelines](CONTRIBUTING.md)
- [Branching Strategy](BRANCHING_STRATEGY.md)
- [Merge Strategy](MERGE_STRATEGY.md)
- [GitHub Flow](https://guides.github.com/introduction/flow/)

## Summary

Branch protection rules ensure:
- ✅ No direct commits to `main`
- ✅ Required pull request reviews (minimum 1)
- ✅ All status checks must pass
- ✅ Branches must be up to date
- ✅ No force pushes to `main`
- ✅ No branch deletion
- ✅ Rules apply to everyone (including admins)

These rules maintain code quality, enable collaboration, and protect the integrity of the `main` branch.

---

For questions about branch protection rules, please create an issue or contact the repository maintainers.
