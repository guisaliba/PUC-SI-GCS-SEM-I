# PUC-SI-GCS-SEM-I

> A comprehensive Configuration Management (CM) repository implementing industry best practices and standards.

## Overview

This repository serves as a theoretical artifact for research about Configuration Management, demonstrating the implementation of professional software development practices, workflows, and standards.

## Configuration Management Practices

This repository implements the following CM strategies and patterns:

### Adopted Strategies

- **[Conventional Commits](https://www.conventionalcommits.org/)**: Structured commit messages for automated versioning and changelog generation
- **[Conventional Branches](BRANCHING_STRATEGY.md)**: Standardized branch naming conventions
- **[Semantic Versioning (SemVer)](VERSIONING.md)**: Clear and predictable version numbering
- **[GitHub Flow](BRANCHING_STRATEGY.md)**: Lightweight, branch-based workflow
- **[Merge Commits](MERGE_STRATEGY.md)**: Preserving complete development history

### Branch Protection

The `main` branch is protected with the following rules:

- ✅ No direct commits allowed
- ✅ No branch deletion allowed
- ✅ Minimum 1 approving review required on pull requests
- ✅ Branches must be up to date before merging
- ✅ All status checks must pass before merging

See [BRANCH_PROTECTION.md](BRANCH_PROTECTION.md) for complete details.

## Documentation

Comprehensive documentation is available for all aspects of the project:

### For Contributors

- **[CONTRIBUTING.md](CONTRIBUTING.md)** - Complete guide on how to contribute to this project
- **[CODE_CONVENTIONS.md](CODE_CONVENTIONS.md)** - Code style and conventions standards
- **[BRANCHING_STRATEGY.md](BRANCHING_STRATEGY.md)** - Branch naming and GitHub Flow workflow
- **[MERGE_STRATEGY.md](MERGE_STRATEGY.md)** - Merge commit strategy and process

### For Maintainers

- **[VERSIONING.md](VERSIONING.md)** - Semantic versioning guidelines and practices
- **[BRANCH_PROTECTION.md](BRANCH_PROTECTION.md)** - Branch protection rules and configuration

### Templates

- **[Pull Request Template](.github/pull_request_template.md)** - Standardized PR format
- **[Bug Report Template](.github/ISSUE_TEMPLATE/bug_report.md)** - For reporting bugs
- **[Feature Request Template](.github/ISSUE_TEMPLATE/feature_request.md)** - For suggesting features

## Quick Start

### For New Contributors

1. Read the [Contributing Guidelines](CONTRIBUTING.md)
2. Review the [Code Conventions](CODE_CONVENTIONS.md)
3. Understand the [Branching Strategy](BRANCHING_STRATEGY.md)
4. Create your feature branch following conventions
5. Make changes following code standards
6. Commit using conventional commits format
7. Submit a pull request using the template

### Example Workflow

```bash
# 1. Clone the repository
git clone https://github.com/guisaliba/PUC-SI-GCS-SEM-I.git
cd PUC-SI-GCS-SEM-I

# 2. Create a feature branch
git checkout -b feature/your-feature-name

# 3. Make changes and commit
git add .
git commit -m "feat: add new feature"

# 4. Push to your fork
git push origin feature/your-feature-name

# 5. Create a Pull Request on GitHub
```

## Project Structure

```
PUC-SI-GCS-SEM-I/
├── .github/
│   ├── ISSUE_TEMPLATE/
│   │   ├── bug_report.md
│   │   └── feature_request.md
│   └── pull_request_template.md
├── CONTRIBUTING.md
├── CODE_CONVENTIONS.md
├── BRANCHING_STRATEGY.md
├── MERGE_STRATEGY.md
├── VERSIONING.md
├── BRANCH_PROTECTION.md
├── LICENSE
├── README.md
└── .gitignore
```

## Development Workflow

This project follows **GitHub Flow**:

1. `main` branch is always deployable
2. Create descriptive feature branches from `main`
3. Commit regularly with conventional commit messages
4. Open pull requests early for feedback
5. Collaborate through code reviews
6. Merge to `main` after approval and passing checks
7. Deploy from `main`

See [BRANCHING_STRATEGY.md](BRANCHING_STRATEGY.md) for detailed workflow information.

## Commit Message Format

We follow the Conventional Commits specification:

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

**Common Types:**
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `style`: Code style changes (formatting, etc.)
- `refactor`: Code refactoring
- `test`: Adding or updating tests
- `chore`: Maintenance tasks

**Example:**
```
feat(auth): add user authentication

Implements JWT-based authentication system with login,
logout, and session management.

Closes #123
```

See [CONTRIBUTING.md](CONTRIBUTING.md#commit-guidelines) for complete commit guidelines.

## Versioning

This project uses [Semantic Versioning (SemVer)](https://semver.org/):

- **MAJOR** version for incompatible API changes
- **MINOR** version for backward-compatible functionality
- **PATCH** version for backward-compatible bug fixes

See [VERSIONING.md](VERSIONING.md) for detailed versioning guidelines.

## Code Review Process

All changes require code review:

1. At least one approving review is required
2. All CI checks must pass
3. Branch must be up to date with `main`
4. No merge conflicts
5. All review comments must be addressed

See [CONTRIBUTING.md](CONTRIBUTING.md#code-review-process) for the complete review process.

## Resources

### Internal Documentation
- [Contributing Guidelines](CONTRIBUTING.md)
- [Code Conventions](CODE_CONVENTIONS.md)
- [Branching Strategy](BRANCHING_STRATEGY.md)
- [Merge Strategy](MERGE_STRATEGY.md)
- [Versioning](VERSIONING.md)
- [Branch Protection](BRANCH_PROTECTION.md)

### External Resources
- [Conventional Commits](https://www.conventionalcommits.org/)
- [Semantic Versioning](https://semver.org/)
- [GitHub Flow](https://guides.github.com/introduction/flow/)
- [Git Documentation](https://git-scm.com/doc)

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contact

For questions or support, please:
- Create an [issue](../../issues/new/choose) using the appropriate template
- Review existing [documentation](#documentation)
- Check [discussions](../../discussions) (if enabled)

---

**Note**: This repository is a theoretical artifact for research about Configuration Management practices in software development.
