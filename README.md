# PUC-SI-GCS-SEM-I

## Repository Rulesets

This repository uses GitHub Rulesets to enforce code quality and commit standards.

### Active Rulesets

1. **production-ruleset** - Protects main and release/**/* branches
2. **commit-metadata-ruleset** - Enforces valid commit author metadata

For detailed information about rulesets configuration and setup, see [RULESETS.md](RULESETS.md).

### Quick Start for Developers

Before making commits, ensure your git configuration includes your name and email:

```bash
git config user.name "Your Name"
git config user.email "your.email@example.com"
```

Optional: Install the pre-commit hook for local validation:

```bash
cp .github/hooks/pre-commit .git/hooks/pre-commit
chmod +x .git/hooks/pre-commit
```

### Automated Checks

All pushes and pull requests to protected branches (main, release/**) are automatically validated for:
- ✅ Valid commit author name
- ✅ Valid commit author email

See the workflow at [.github/workflows/commit-metadata-validation.yml](.github/workflows/commit-metadata-validation.yml)