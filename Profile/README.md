# Sakani-Shokran - Graduation Project

A roommate / apartment matching and rental platform.

## Repositories

| Repo | Description | Stack |
|------|-------------|-------|
| `backend` | REST API and business logic | .NET |
| `frontend` | Web application | React |
| `mobile` | Mobile application | Flutter |

## Workflow at a glance

1. Pick or create an Issue and assign it to yourself.
2. Create a branch from `dev` named `feature/<short-description>`.
3. Commit using Conventional Commits (see below).
4. Open a Pull Request into `dev`, link the issue, and request a review.
5. At least 1 approval and passing checks are required before merging.
6. `dev` is merged into `main` for each release.

Full details: [CONTRIBUTING.md](../CONTRIBUTING.md)

## Branching strategy

| Branch | Purpose | Created from | Merges into |
|--------|---------|--------------|-------------|
| `main` | Stable, production-ready code | - | - |
| `dev` | Integration branch for the next release | `main` | `main` |
| `feature/*` | New features | `dev` | `dev` |
| `fix/*` | Bug fixes | `dev` | `dev` |
| `hotfix/*` | Urgent production fixes | `main` | `main` and `dev` |
| `release/*` | Release preparation (optional) | `dev` | `main` and `dev` |

Naming: lowercase, hyphen-separated, short. Examples: `feature/user-login`, `fix/roommate-filter-null`, `hotfix/jwt-expiry`.

## Commit message format

```
<type>[optional scope]: <Description>

[optional body]

[optional footer(s)]
```

Example: `feat(auth): Add JWT refresh token endpoint`

Types: `feat`, `fix`, `refactor`, `perf`, `docs`, `style`, `test`, `build`, `ci`, `chore`, `ops`, `revert`.

## Contact

Questions? Open an Issue.
