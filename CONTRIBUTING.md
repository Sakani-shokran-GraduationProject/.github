# Contributing Guide

This guide applies to all repositories in the organization (`backend`, `frontend`, `mobile`, ...).

---

## 1. Why we care about commit messages

- Future readers understand what changed and why.
- Changes are easier to find and to undo.
- Release notes can be generated from history.

A message like `Tweaked a few things` tells nobody anything. Six months later, not even you will remember.

---

## 2. Commit message convention (Conventional Commits)

```
<type>[optional scope]: <Description>

[optional body]

[optional footer(s)]
```

### Types

| Type | Use it for |
|------|-----------|
| `feat` | A new feature |
| `fix` | A bug fix |
| `refactor` | Restructuring code without changing behavior or fixing a bug |
| `perf` | Performance improvements |
| `docs` | Documentation only (README, comments) |
| `style` | Formatting only (whitespace, semicolons), no logic change |
| `test` | Adding or fixing tests |
| `build` | Build system, dependencies, project version |
| `ci` | CI/CD pipeline changes |
| `ops` | Infrastructure, deployment, backup |
| `chore` | Misc. changes that don't touch src/tests (e.g. `.gitignore`) |
| `revert` | Reverting a previous commit |

### Rules

1. Subject line must be 50 characters or fewer.
2. Capitalize the description.
3. No period at the end of the subject line.
4. Use the imperative mood: "Add", "Fix", "Update", not "Added" or "Adding".
5. Separate the subject from the body with a blank line.
6. Wrap the body at 72 characters.
7. Use the body to explain what and why, not how.
8. Reference issues in the footer: `Closes #12`.

### Examples

Good:

```
feat(auth): Add JWT refresh token endpoint
fix(matching): Handle null budget in roommate filter
docs: Update API setup instructions
refactor(listing): Extract price calculation into service
```

With body and footer:

```
fix(booking): Prevent double booking of the same apartment

Two users could book the same apartment at the same time because the
availability check and the insert were not in one transaction.
Wrap both in a single transaction.

Closes #34
```

Bad:

```
Tweaked a few things
fixed bug
update
WIP
```

### Fixing your last commit

```bash
git commit --amend
```

Only amend commits that are not pushed yet. Never rewrite history on shared branches.

---

## 3. Branching strategy

```
main      *-----------*-----------*   (production, tagged releases)
           \         / \         /
dev         *--*--*--*   *--*--*--*   (integration)
             \  /         \  /
feature/*     **           **
```

| Branch | Purpose | Branch from | Merge into |
|--------|---------|-------------|------------|
| `main` | Stable, production-ready | - | - |
| `dev` | Integration for the next release | `main` | `main` |
| `feature/<name>` | New functionality | `dev` | `dev` |
| `fix/<name>` | Non-urgent bug fixes | `dev` | `dev` |
| `hotfix/<name>` | Urgent production fix | `main` | `main` and `dev` |
| `release/<version>` | Final polish before release (optional) | `dev` | `main` and `dev` |

### Branch naming

- Prefix plus a short, lowercase, hyphen-separated description.
- Include the issue number when possible.

```
feature/42-user-login
fix/57-roommate-filter-null
hotfix/jwt-expiry
```

### Golden rules

- Never push directly to `main` or `dev`. Always use a Pull Request.
- One branch = one purpose. Keep branches short-lived.
- Pull the latest `dev` before starting and before opening a PR: `git pull origin dev`.

---

## 4. Pull request process

1. Create a branch from `dev`.
2. Make small, focused commits following the convention above.
3. Push and open a PR into `dev` (or `main` for hotfixes).
4. The PR title follows the same format as a commit: `feat(auth): Add JWT refresh token endpoint`.
5. Fill in the description: what changed, why, how to test, linked issue (`Closes #id`).
6. Request a review. At least 1 approval is required.
7. All checks must pass and conversations must be resolved.
8. Merge using Squash and merge for features and fixes (keeps `dev` history clean).
9. Delete the branch after merging.

### PR checklist

- [ ] Code builds and runs locally
- [ ] Tests added/updated and passing
- [ ] No secrets, keys or connection strings committed
- [ ] Docs updated if behavior changed
- [ ] PR linked to an issue

---

## 5. Recommended branch protection (`main` and `dev`)

- Require a pull request before merging
- Require at least 1 approval
- Require status checks to pass
- Require conversation resolution
- Block force pushes and branch deletion
