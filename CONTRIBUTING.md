# Contributing Guide

This document defines the Git branching, review, and release workflow for this project. All contributors must follow this process for every change.

## Branch Structure

- **`main`** — Production branch. Always stable and deployable. Protected.
- **`develop`** — Integration branch. All finished features/fixes land here first for testing. Protected.
- **`feature/*`** — New features. Branched from `develop`.
- **`fix/*`** — Non-critical bug fixes. Branched from `develop`.
- **`hotfix/*`** — Urgent production fixes. Branched from `main`, merged into **both** `main` and `develop`.

Direct pushes to `main` and `develop` are disabled. All changes must go through a Pull Request.

## Branch Naming Convention

```
feature/TICKET-ID-short-description
fix/TICKET-ID-short-description
hotfix/TICKET-ID-short-description
```

Example: `feature/PROJ-142-user-avatar-upload`

## Commit Message Convention

Format: `type(scope): short description`

Common types: `feat`, `fix`, `hotfix`, `docs`, `chore`, `refactor`, `test`

Examples:
```
feat(auth): add password reset flow
fix(cart): correct tax calculation on checkout
hotfix(payments): patch webhook signature bypass
docs: update contributing guide
```

## Standard Workflow (Feature/Fix)

1. Create a branch from `develop`:
   ```bash
   git checkout develop
   git pull
   git checkout -b feature/TICKET-ID-description
   ```
2. Develop and test locally.
3. Push the branch:
   ```bash
   git push -u origin feature/TICKET-ID-description
   ```
4. Open a Pull Request into `develop`.
5. Address review comments and resolve all conversations.
6. Once approved and checks pass, merge using **Squash and Merge**.
7. Delete the branch after merging.

## Hotfix Workflow

Used only for urgent production issues.

1. Create a branch from `main`:
   ```bash
   git checkout main
   git pull
   git checkout -b hotfix/TICKET-ID-description main
   ```
2. Apply and test the fix.
3. Push and open **two Pull Requests**:
   - One into `main` (ships the fix to production)
   - One into `develop` (keeps develop in sync so the fix isn't lost in the next release)
4. Get both reviewed, approved, and merged.

## Pull Request Requirements

Every PR must include:
- Ticket ID
- Clear title
- Description of changes
- Testing performed
- Screenshots/video for UI changes (if applicable)
- Known issues or limitations

## Review & Merge Rules

- Minimum 1 reviewer approval required before merging.
- PR authors cannot approve their own PRs (enforced by GitHub).
- All review conversations must be resolved before merging.
- Required CI checks (where configured) must pass before merging.
- Use **Squash and Merge** for feature/fix PRs into `develop`.
- Keep feature branches up to date with `develop` during long-running work.

## Never Commit

- Secrets, API keys, or passwords
- `.env` files
- Any sensitive credentials