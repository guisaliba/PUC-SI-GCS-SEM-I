# GitHub Configuration

## Automatic Branch Deletion

This repository is configured to automatically delete branches after they are merged to keep the repository clean and organized.

### Protected Branches

The following branches are **protected** and will **NOT** be deleted automatically:

- `main` - Main production branch
- `dev` / `development` - Development branch
- `release/**` - Any release branches (e.g., `release/v1.0.0`, `release/2024-01`, etc.)

### Automatic Deletion

All other branches (feature branches, bugfix branches, hotfix branches, etc.) will be automatically deleted when their pull requests are merged. This includes branches following conventional naming patterns such as:

- `feature/*`
- `feat/*`
- `bugfix/*`
- `fix/*`
- `hotfix/*`
- `chore/*`
- `docs/*`
- Any other custom branch names

### How It Works

The deletion is handled by the GitHub Actions workflow located at `.github/workflows/delete-merged-branches.yml`. This workflow:

1. Triggers when a pull request is closed
2. Checks if the PR was actually merged (not just closed without merging)
3. Verifies if the branch name matches any protected patterns
4. Deletes the branch if it's not protected
5. Preserves the branch if it matches protected patterns

### Manual Override

If you need to preserve a specific branch temporarily, you can:

1. Avoid merging its PR until you're ready for it to be deleted, OR
2. Name it starting with `release/` to protect it, OR
3. Manually restore it after deletion if needed (within 30 days in GitHub)

### Benefits

- Keeps the repository clean and organized
- Reduces clutter in branch lists
- Automatically enforces branch hygiene
- No manual cleanup required after merging PRs
