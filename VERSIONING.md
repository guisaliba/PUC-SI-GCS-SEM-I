# Semantic Versioning (SemVer)

This document describes how we use Semantic Versioning (SemVer) for version management in this project.

## Table of Contents

- [Overview](#overview)
- [Version Format](#version-format)
- [Version Increment Rules](#version-increment-rules)
- [Versioning Workflow](#versioning-workflow)
- [Pre-release Versions](#pre-release-versions)
- [Build Metadata](#build-metadata)
- [Best Practices](#best-practices)
- [Examples](#examples)

## Overview

**Semantic Versioning (SemVer)** is a versioning scheme that conveys meaning about the underlying changes with each new release. It helps users understand the impact of upgrading to a new version.

### Key Principles

- Version numbers and the way they change convey meaning
- Once a versioned package has been released, the contents must not be modified
- Any modifications must be released as a new version
- Breaking changes must increase the major version

### Benefits

- **Predictability**: Users know what to expect from version changes
- **Compatibility**: Clear indication of backward compatibility
- **Communication**: Version numbers communicate the nature of changes
- **Dependency Management**: Easier to manage dependencies with clear versioning

## Version Format

### Standard Format

```
MAJOR.MINOR.PATCH
```

Example: `1.4.2`

- **MAJOR**: `1` - Major version (breaking changes)
- **MINOR**: `4` - Minor version (new features, backward compatible)
- **PATCH**: `2` - Patch version (bug fixes, backward compatible)

### Version Components

| Component | Description | When to Increment |
|-----------|-------------|-------------------|
| **MAJOR** | Breaking changes | Incompatible API changes |
| **MINOR** | New features | Backward-compatible functionality |
| **PATCH** | Bug fixes | Backward-compatible bug fixes |

## Version Increment Rules

### MAJOR Version (X.0.0)

Increment when you make **incompatible API changes** or **breaking changes**.

**Examples of breaking changes:**
- Removing or renaming public APIs
- Changing function signatures
- Modifying expected behavior of existing features
- Removing support for a platform or language version
- Changing data structures in incompatible ways
- Removing configuration options

**Commit Types:**
- Any commit with `BREAKING CHANGE:` in footer
- Commits with `!` after type/scope: `feat!:`, `fix!:`

**Example:**
```
Version: 1.5.3 → 2.0.0

feat!: redesign authentication API

BREAKING CHANGE: The auth module now uses token-based 
authentication instead of session-based. All existing 
authentication code needs to be updated.
```

### MINOR Version (0.X.0)

Increment when you add **new features** in a **backward-compatible** manner.

**Examples of minor changes:**
- Adding new public APIs
- Adding new optional parameters to functions
- Adding new features or functionality
- Marking features as deprecated (but still working)
- Introducing substantial new functionality in private code

**Commit Types:**
- `feat:` - New features

**Example:**
```
Version: 1.5.3 → 1.6.0

feat(auth): add two-factor authentication support

Adds optional 2FA support while maintaining backward 
compatibility with existing single-factor authentication.
```

### PATCH Version (0.0.X)

Increment when you make **backward-compatible bug fixes**.

**Examples of patch changes:**
- Fixing bugs
- Performance improvements
- Internal refactoring
- Documentation updates
- Dependency updates (without new features)

**Commit Types:**
- `fix:` - Bug fixes
- `perf:` - Performance improvements
- `refactor:` - Code refactoring (no functional changes)
- `docs:` - Documentation only changes
- `style:` - Code style changes
- `test:` - Adding or updating tests
- `chore:` - Maintenance tasks

**Example:**
```
Version: 1.5.3 → 1.5.4

fix(auth): resolve login timeout issue

Fixes a bug where login would timeout after 30 seconds
on slow connections.
```

## Versioning Workflow

### Initial Development (0.x.x)

- Start with version `0.1.0` for initial development
- Major version zero (0.y.z) is for initial development
- Anything may change at any time
- Public API should not be considered stable

```
0.1.0 - Initial development
0.2.0 - Add new features
0.3.0 - Add more features
0.9.0 - Feature complete, testing
1.0.0 - First stable release
```

### Stable Releases (1.0.0+)

Once you release version `1.0.0`, you declare the public API stable:
- MAJOR version must be incremented for breaking changes
- MINOR version for new features
- PATCH version for bug fixes

### Creating a Release

1. **Determine Version Bump**
   - Review commits since last release
   - Identify highest impact change (breaking/feature/fix)
   - Apply appropriate version increment

2. **Update Version Number**
   ```bash
   # Using npm (for Node.js projects)
   npm version major  # 1.5.3 → 2.0.0
   npm version minor  # 1.5.3 → 1.6.0
   npm version patch  # 1.5.3 → 1.5.4
   ```

3. **Create Release Notes**
   - Document all changes since last release
   - Group by type (Breaking Changes, Features, Bug Fixes)
   - Include migration guide for breaking changes

4. **Tag the Release**
   ```bash
   git tag -a v1.6.0 -m "Release version 1.6.0"
   git push origin v1.6.0
   ```

5. **Publish Release**
   - Create GitHub release from tag
   - Include release notes
   - Attach built artifacts if applicable

## Pre-release Versions

### Format

```
MAJOR.MINOR.PATCH-PRERELEASE
```

### Pre-release Identifiers

- **alpha**: Early testing version, unstable
- **beta**: Feature complete, but may have bugs
- **rc** (release candidate): Potentially final, unless significant bugs emerge

### Examples

```
1.0.0-alpha.1
1.0.0-alpha.2
1.0.0-beta.1
1.0.0-beta.2
1.0.0-rc.1
1.0.0-rc.2
1.0.0
```

### Pre-release Workflow

```bash
# Alpha releases (internal testing)
1.0.0-alpha.1  # Initial alpha
1.0.0-alpha.2  # Second alpha
1.0.0-alpha.3  # Third alpha

# Beta releases (wider testing)
1.0.0-beta.1   # Feature complete
1.0.0-beta.2   # Bug fixes

# Release candidates (final testing)
1.0.0-rc.1     # First release candidate
1.0.0-rc.2     # Final release candidate

# Stable release
1.0.0          # Production ready
```

## Build Metadata

Build metadata can be appended with a plus sign:

```
1.0.0+20251022
1.0.0+sha.abc123
1.0.0-beta.1+exp.sha.5114f85
```

Build metadata:
- SHOULD be ignored when determining version precedence
- Denotes build or commit information
- Useful for CI/CD tracking

## Best Practices

### Do's ✅

1. **Start with 0.1.0** for initial development
2. **Release 1.0.0** when public API is stable
3. **Document breaking changes** clearly
4. **Use tags** for all releases
5. **Create release notes** for each version
6. **Follow conventional commits** to automate versioning
7. **Increment only one number** per release (except when resetting)
8. **Reset lower numbers** when incrementing higher ones
   - `1.5.3` → `2.0.0` (reset minor and patch)
   - `1.5.3` → `1.6.0` (reset patch)

### Don'ts ❌

1. **Don't modify released versions** - always create new version
2. **Don't skip versions** - increment sequentially
3. **Don't use dates** as version numbers (not SemVer)
4. **Don't make breaking changes** in minor or patch releases
5. **Don't release** without testing
6. **Don't forget** to update changelog
7. **Don't mix** different versioning schemes

### Version Numbering Guidelines

```
# Good
1.0.0
1.1.0
1.1.1
1.2.0
2.0.0

# Bad
1.0
1.2.3.4
2024.10.22
1.2.3-latest
```

## Examples

### Example 1: Bug Fix Release

```
Current version: 1.4.2

Changes:
- fix(api): resolve null pointer exception
- fix(ui): correct button alignment

New version: 1.4.3
```

### Example 2: Feature Release

```
Current version: 1.4.3

Changes:
- feat(export): add CSV export functionality
- feat(search): add advanced search filters
- fix(pagination): resolve page navigation issue

New version: 1.5.0
```

### Example 3: Breaking Change Release

```
Current version: 1.5.0

Changes:
- feat!: redesign configuration system
  BREAKING CHANGE: Configuration file format changed from JSON to YAML
- feat(api): add new endpoints
- fix(security): patch security vulnerability

New version: 2.0.0
```

### Example 4: Pre-release Flow

```
Current stable: 1.5.0

Development cycle:
1. 1.6.0-alpha.1  # Start development
2. 1.6.0-alpha.2  # Continue development
3. 1.6.0-beta.1   # Feature complete
4. 1.6.0-beta.2   # Bug fixes
5. 1.6.0-rc.1     # Release candidate
6. 1.6.0          # Stable release
```

## Automation

### Using Conventional Commits

Conventional commits can automate version determination:

```bash
# These commits would trigger PATCH bump
fix: resolve login issue
perf: improve query performance

# These commits would trigger MINOR bump
feat: add user profile page

# These commits would trigger MAJOR bump
feat!: redesign API structure
fix!: change database schema

BREAKING CHANGE: API endpoints restructured
```

### Automated Tools

Consider using tools for automation:
- **semantic-release**: Automates versioning and release
- **standard-version**: Generates changelog and determines version
- **commitizen**: Helps write conventional commits
- **conventional-changelog**: Generates changelog from commits

## Integration with Git

### Tagging Strategy

```bash
# Create annotated tag
git tag -a v1.5.0 -m "Release version 1.5.0"

# Push tag to remote
git push origin v1.5.0

# List all tags
git tag -l

# Checkout specific version
git checkout v1.5.0
```

### Release Branches (if needed)

For long-term support:

```
main (2.x development)
├── release/1.x (1.x maintenance)
    ├── v1.5.0
    ├── v1.5.1
    └── v1.5.2
```

## Version Dependencies

When specifying dependencies, use appropriate version ranges:

### NPM/Node.js Example

```json
{
  "dependencies": {
    "exact-version": "1.5.3",           // Exact version
    "minor-updates": "^1.5.3",          // >= 1.5.3 < 2.0.0
    "patch-updates": "~1.5.3",          // >= 1.5.3 < 1.6.0
    "range": ">=1.5.0 <2.0.0"          // Version range
  }
}
```

## Changelog

Maintain a `CHANGELOG.md` file with each release:

```markdown
# Changelog

## [2.0.0] - 2025-10-22

### Breaking Changes
- Redesigned authentication API

### Added
- Two-factor authentication support

### Fixed
- Login timeout on slow connections

## [1.5.0] - 2025-10-15

### Added
- CSV export functionality
- Advanced search filters

### Fixed
- Page navigation issue
```

## References

- [Semantic Versioning Specification](https://semver.org/)
- [Conventional Commits](https://www.conventionalcommits.org/)
- [Keep a Changelog](https://keepachangelog.com/)
- [Contributing Guidelines](CONTRIBUTING.md)
- [Branching Strategy](BRANCHING_STRATEGY.md)

---

Following semantic versioning ensures clear communication about the nature and impact of changes in each release.
