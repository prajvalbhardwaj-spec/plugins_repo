# git-commit-helper

A Claude Code plugin that generates descriptive, Conventional Commits-compliant commit messages by analyzing your staged git diff.

## What it does

Type `/git-commit-helper:git-commit-helper` (or set up a shorter alias) and Claude will:
- Inspect your staged changes via `git diff --staged`
- Identify the change type, scope, and intent
- Write a headline ≤ 72 chars in `<type>(<scope>): <description>` format
- Add a bulleted body explaining the **why** for non-trivial changes

## Installation

```bash
# Install directly from GitHub
claude plugin add https://github.com/prajvalbhardwaj-spec/plugins_repo
```

## Usage

Stage your changes as usual, then invoke the skill:

```bash
git add .
# Inside Claude Code:
/git-commit-helper:git-commit-helper
```

Claude will analyze the diff and propose a commit message you can edit before committing.

## Commit Message Rules

- Follows the [Conventional Commits](https://www.conventionalcommits.org/) specification
- Headlines capped at 72 characters
- Imperative mood only ("add", "fix" — not "added", "fixed")
- Body focuses on intent and impact, not line-by-line description
- Breaking changes are flagged with a `BREAKING CHANGE:` footer

## Repository

[https://github.com/prajvalbhardwaj-spec/plugins_repo](https://github.com/prajvalbhardwaj-spec/plugins_repo)

## Plugin Structure

```
plugins_repo/
├── .claude-plugin/
│   └── marketplace.json     # Registry manifest
└── plugins/
    └── git-commit-helper/
        ├── skills/
        │   └── git-commit-helper/
        │       └── SKILL.md # Skill instructions for Claude
        └── README.md
```
