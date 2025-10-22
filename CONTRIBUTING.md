# Contributing to PUC-SI-GCS-SEM-I

Thank you for your interest in contributing to this project! This document provides guidelines and instructions for contributing to this repository.

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [Getting Started](#getting-started)
- [How to Contribute](#how-to-contribute)
- [Development Workflow](#development-workflow)
- [Commit Guidelines](#commit-guidelines)
- [Pull Request Process](#pull-request-process)
- [Code Review Process](#code-review-process)

## Code of Conduct

By participating in this project, you are expected to uphold our code of conduct:
- Be respectful and inclusive
- Welcome newcomers and help them get started
- Focus on what is best for the community
- Show empathy towards other community members

## Getting Started

1. Fork the repository
2. Clone your fork locally
3. Set up the upstream remote:
   ```bash
   git remote add upstream https://github.com/guisaliba/PUC-SI-GCS-SEM-I.git
   ```
4. Create a new branch following our [branching strategy](BRANCHING_STRATEGY.md)

## How to Contribute

### Reporting Bugs

If you find a bug, please create an issue using the bug report template. Include:
- A clear and descriptive title
- Steps to reproduce the issue
- Expected behavior
- Actual behavior
- Screenshots (if applicable)
- Environment details

### Suggesting Enhancements

Feature requests are welcome! Please create an issue using the feature request template and include:
- A clear and descriptive title
- Detailed description of the proposed feature
- Rationale for why this feature would be useful
- Examples of how it would work

### Contributing Code

1. Check existing issues and pull requests to avoid duplicates
2. Create or comment on an issue to discuss your proposed changes
3. Fork the repository and create a branch from `main`
4. Make your changes following our [code conventions](CODE_CONVENTIONS.md)
5. Write or update tests as needed
6. Ensure your code passes all tests and linting
7. Commit your changes following [commit guidelines](#commit-guidelines)
8. Push to your fork and submit a pull request

## Development Workflow

This project follows the **GitHub Flow** workflow:

1. The `main` branch is always deployable and protected
2. Create a new branch from `main` for each feature or fix
3. Regularly commit to your branch
4. Open a pull request early for feedback
5. After review and approval, merge to `main`
6. Deploy from `main`

See [BRANCHING_STRATEGY.md](BRANCHING_STRATEGY.md) for detailed information.

## Commit Guidelines

We follow the **Conventional Commits** specification. Each commit message should be structured as follows:

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

### Commit Types

- **feat**: A new feature
- **fix**: A bug fix
- **docs**: Documentation only changes
- **style**: Changes that don't affect code meaning (formatting, missing semicolons, etc.)
- **refactor**: Code change that neither fixes a bug nor adds a feature
- **perf**: Performance improvement
- **test**: Adding or correcting tests
- **chore**: Changes to build process or auxiliary tools
- **ci**: Changes to CI configuration files and scripts
- **build**: Changes that affect the build system or external dependencies

### Examples

```
feat(auth): add user authentication
fix(api): resolve null pointer exception in user service
docs(readme): update installation instructions
style(components): format code according to style guide
refactor(database): optimize query performance
test(auth): add unit tests for login functionality
chore(deps): update dependencies to latest versions
```

### Commit Message Guidelines

- Use the imperative mood ("add" not "added" or "adds")
- Keep the first line under 72 characters
- Reference issues and pull requests when relevant
- Use the body to explain what and why, not how

## Pull Request Process

1. **Before submitting:**
   - Ensure your branch is up to date with `main`
   - Run all tests and ensure they pass
   - Update documentation as needed
   - Follow the code conventions

2. **Creating the PR:**
   - Use the pull request template
   - Provide a clear title following conventional commit format
   - Describe what changes you made and why
   - Reference any related issues
   - Add appropriate labels

3. **Requirements:**
   - All CI checks must pass
   - At least one approving review is required
   - Branch must be up to date with `main` before merging
   - No merge conflicts

4. **Merging:**
   - Only **merge commits** are allowed (no squash or rebase merges)
   - Delete your branch after merging
   - The maintainer will merge your PR after approval

See [MERGE_STRATEGY.md](MERGE_STRATEGY.md) for detailed information.

## Code Review Process

### For Contributors

- Be open to feedback and suggestions
- Respond to review comments promptly
- Make requested changes in new commits (don't force push)
- Mark conversations as resolved after addressing them

### For Reviewers

- Review PRs promptly (within 48 hours when possible)
- Be constructive and respectful in feedback
- Focus on:
  - Code quality and maintainability
  - Adherence to conventions and standards
  - Test coverage
  - Documentation completeness
  - Security implications
- Approve when satisfied, or request changes with clear explanations

## Additional Resources

- [Code Conventions](CODE_CONVENTIONS.md)
- [Branching Strategy](BRANCHING_STRATEGY.md)
- [Merge Strategy](MERGE_STRATEGY.md)
- [Versioning](VERSIONING.md)
- [Branch Protection Rules](BRANCH_PROTECTION.md)

## Questions?

If you have questions or need help, please:
- Check existing documentation
- Search existing issues
- Create a new issue if needed

Thank you for contributing!
