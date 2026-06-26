---
name: "git-commit-helper"
description: "Generate descriptive commit messages by analyzing git diffs. Use when the user asks for help writing commit messages or reviewing staged changes."
---

# Git Commit Helper Skill

## Context & Purpose
Always write commit messages following the Conventional Commits standard.

## Process Workflow
1. Run `git diff --staged` to inspect all staged changes (if the user hasn't already provided a diff).
2. Identify the core architectural change: what type is it? (feat, fix, refactor, chore, docs, test, style, perf, ci, build).
3. Determine the scope from the files changed (e.g., `auth`, `api`, `ui`, `db`).
4. Write a clear, short imperative headline in the format: `<type>(<scope>): <short description>`.
5. If the change is non-trivial, add a blank line followed by a bulleted body explaining the **why**, not just the **what**.

## Commit Message Format
```
<type>(<scope>): <short description>

- Why this change was needed
- What problem it solves or what behavior it introduces
- Any important side effects or caveats
```

### Valid types
| Type       | Use for                                         |
|------------|-------------------------------------------------|
| `feat`     | A new feature                                   |
| `fix`      | A bug fix                                       |
| `refactor` | Code change that neither fixes a bug nor adds a feature |
| `docs`     | Documentation only changes                      |
| `test`     | Adding or updating tests                        |
| `chore`    | Build process, tooling, or dependency updates   |
| `style`    | Formatting, missing semi-colons, etc.           |
| `perf`     | Performance improvement                         |
| `ci`       | CI/CD configuration changes                     |
| `build`    | Build system changes                            |

## Rules & Constraints
- The headline must not exceed **72 characters**.
- Use the **imperative mood** in the headline ("add", "fix", "remove" — not "added", "fixes", "removed").
- Never use vague headlines like "minor fixes", "update", "WIP", or "changes".
- Body lines must not exceed **72 characters** each.
- Do **not** describe what the code does line-by-line — focus on intent and impact.
- If there are **breaking changes**, add a footer: `BREAKING CHANGE: <description>`.

## Examples

### Simple change
```
fix(auth): prevent token refresh loop on 401 response
```

### Complex change with body
```
feat(api): add rate limiting to public endpoints

- Protects against abuse and ensures fair usage across clients
- Defaults to 100 req/min per IP, configurable via env var RATE_LIMIT
- Returns 429 with Retry-After header when limit is exceeded
```

### Breaking change
```
refactor(db): replace raw SQL queries with ORM layer

- Eliminates manual query construction and reduces injection risk
- All callers now use typed model methods instead of db.query()

BREAKING CHANGE: db.query() is removed; migrate callers to model methods
```
